<template>
    <div class="app">
        <h1>Страница с постами</h1>
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
        
        <post-list v-bind:posts="posts" @remove="removePost"
        v-if="!isPostsLoading">
        </post-list>
        <div v-else>Идет загрузка...</div>
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
            posts: [

            ],
            id: "",
            title: "",
            body: "",
            dialogVisible:false,
            isPostsLoading: false,
            selectedSort: '',
            sortOptions:[
                {value: 'title', name: 'По названию'},
                {valie: 'body', name: 'По содержанию'}
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
        async fetchPosts(){
            try{
                this.isPostsLoading = true;
                const response = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=10');
                this.posts = response.data;
                
            }catch(e){
                alert('Error')
            } finally{
                this.isPostsLoading = false;
            }
        }
    },
    mounted(){
        this.fetchPosts();
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
</style>