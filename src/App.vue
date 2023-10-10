<template>
    <div class="app">
        <h1>Страница с постами</h1>
        <my-input v-model="searchQuery"
        @input="searchQuery = $event.target.value"
        placeholder="Search..."
        >
        </my-input>
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
        <div class="observer" ref="observer"></div>
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
        const options = {
            rootMargin: '0px',
            threshold: 1.0
        }
        const callback = (entries, observer) => {
            if(entries[0].isIntersecting && this.page < this.totalPage){
                this.loadMorePosts();
            }
        }
        const observer = new IntersectionObserver(callback, options);
        observer.observe(this.$refs.observer);
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
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

.app {
    padding: 20px;
}
.loader{
    position: absolute;
}
.app_buttons{
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
    height: 30px;
    background: green;
}
</style>