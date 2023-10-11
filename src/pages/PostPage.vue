<template>
    <div>
        <h1>Страница с постами</h1>
        <div class="input_search">
            <my-input v-model="searchQuery"
            @input="searchQuery = $event.target.value"
            placeholder="Search..."
            style="width:100%"
            v-focus
            >
            </my-input>
        </div>
        
        <div class="app_buttons">
            <my-button
                @click="showDialog">Добавить пост
            </my-button>
            <my-select
                v-model="selectedSort"
                :options="sortOptions"
            >

            </my-select>
        </div>
        
        <my-dialog v-model:show="dialogVisible">
            <post-form @create="createPost">

            </post-form>
        </my-dialog>
        
        <post-list v-bind:posts="sortedAndSearchedPosts" @remove="removePost"
        v-if="!isPostsLoading">
        </post-list>
        <div v-else>Идет загрузка...</div>
        <div v-intersection="loadMorePosts" ref="observer"><span v-if="(this.page < this.totalPage && sortedAndSearchedPosts.length > 0)" class="loader"></span></div>
        <!-- <div class="observer" ref="observer"><span v-if="(this.page < this.totalPage && sortedAndSearchedPosts.length > 0)" class="loader"></span></div> -->
        <!-- <div class="paginate">
            <div v-for="pageNumber in totalPage" :key="pageNumber" class="page" :class="{
                'current-page': page === pageNumber
            }"
            @click="changePage(pageNumber)">{{pageNumber}}</div>
        </div> -->
    </div>
</template>

<script>
import PostForm from "@/components/PostForm.vue";
import PostList from "@/components/PostList.vue";
import axios from "axios";
export default {
    components: {
        PostForm, PostList,
    },
    data() {
        return {
            posts: [{id: 1, title: 'title', body: 'body'}],
            id: "",
            title: "",
            body: "",
            dialogVisible:false,
            isPostsLoading: false,
            searchQuery: '',
            selectedSort: '',
            page: 1,
            limit: 10,
            totalPage: 0,
            sortOptions:[
                {value: 'title', name: 'По названию'},
                {value: 'body', name: 'По содержанию'}
            ]
        }
    },
    methods: {
        createPost(post) {
            if (post.title != "" && post.body != "") {
                this.posts.push(post);
                this.dialogVisible = false;
            }
        },
        removePost(post) {
            this.posts = this.posts.filter(p => p.id !== post.id);
        },
        showDialog(){
            this.dialogVisible = true;
        },
        // changePage(pageNumber){
        //     this.page = pageNumber;
        //     // this.fetchPosts();
        // },
        async fetchPosts(){
            try{
                this.isPostsLoading = true;
                const response = await axios.get('https://jsonplaceholder.typicode.com/posts',{
                    params: {
                        _page: this.page,
                        _limit: this.limit,
                    }
                });
                this.totalPage = Math.ceil(response.headers['x-total-count'] / this.limit);
                this.posts = response.data;
                
            }catch(e){
                alert('Error')
            } finally{
                this.isPostsLoading = false;
            }
        },
        async loadMorePosts(){
            try{
                this.page += 1;
                const response = await axios.get('https://jsonplaceholder.typicode.com/posts',{
                    params: {
                        _page: this.page,
                        _limit: this.limit,
                    }
                });
                this.totalPage = Math.ceil(response.headers['x-total-count'] / this.limit);
                this.posts = [...this.posts, ...response.data];
                
            }catch(e){
                alert('Error')
            } 
        }
    },
    mounted(){
        this.fetchPosts();
        console.log(this.$refs.observer);
        // const options = {
        //     rootMargin: '0px',
        //     threshold: 1.0
        // }
        // const callback = (entries, observer) => {
        //     if(entries[0].isIntersecting && this.page < this.totalPage){
        //         this.loadMorePosts();
        //     }
        // }
        // const observer = new IntersectionObserver(callback, options);
        // observer.observe(this.$refs.observer);
    },
    watch: {
        selectedSort(newValue){
            console.log(newValue);
            this.posts.sort((post1,post2)=>{
                return post1[newValue]?.localeCompare(post2[newValue]);
            });
        },
        // page(){
        //     this.fetchPosts();
        // }
    },
    computed: {
        sortedPosts(){
            return [...this.posts].sort((post1, post2)=> post1[this.selectedSort]?.localeCompare(post2[this.selectedSort]));
        },
        sortedAndSearchedPosts(){
            return this.sortedPosts.filter(post => post.title.toLowerCase().includes(this.searchQuery.toLowerCase()));
        }
    }
}
</script>

<style>

.loader{
    position: absolute;
}
.app_buttons{
    display: flex;
    justify-content: space-between;
    margin:25px;
}
.input_search{
    display: flex;
    justify-content: space-between;
    margin:25px;
}

.paginate{
    display: flex;
    margin-top: 15px;
}
.page{
    border: 1px solid black;
    padding: 10px;
}
.current-page{
    border: 2px solid teal;
}
.observer{
    height: 50px;
}


.loader {
  width: 48px;
  height: 48px;
  border-radius: 50%;
  display: block;
  position: relative;
  margin-left: auto;
    margin-right: auto;
  border: 3px solid;
  border-color: teal teal transparent;
  box-sizing: border-box;
  animation: rotation 1s linear infinite;
}
.loader::after {
  content: '';  
  box-sizing: border-box;
  position: absolute;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
  margin: auto;
  border: 3px solid;
  border-color: transparent #FF3D00 #FF3D00;
  width: 24px;
  height: 24px;
  border-radius: 50%;
  animation: rotationBack 0.5s linear infinite;
  transform-origin: center center;
}

@keyframes rotation {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
} 
    
@keyframes rotationBack {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(-360deg);
  }
}
    
</style>