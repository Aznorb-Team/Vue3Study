<template>
    <div class="app">
        <div>
            <form @submit.prevent>
                <h4>Создание поста</h4>
                <input v-bind:value="title" @input="title = $event.target.value" class="input" type="text" name="" id="" placeholder="Название">
                <input v-bind:value="body" @input="body = $event.target.value" class="input" type="text" name="" id="" placeholder="Описание">
                <button class="btn" @click="createPost">Создать</button>
            </form>
        </div>
        <div class="post" v-for="post in posts" :key="post.id">
            <div><strong>Название:</strong> {{ post.title }}</div>
            <div><strong>Описание:</strong> {{ post.body }}</div>
        </div>
    </div>
</template>

<script>
    export default{
        data(){
            return{
                posts: [
                    { id: 1, title: 'Название 1', body: 'Описание 1'},
                    { id: 2, title: 'Название 2', body: 'Описание 2'},
                    { id: 3, title: 'Название 3', body: 'Описание 3'},
                    { id: 4, title: 'Название 4', body: 'Описание 4'},
                ],
                title: "",
                body: "",
            }
        },
        methods: {
            createPost(){
                const newPost = {
                    id: Date.now(),
                    title: this.title,
                    body: this.body,
                }
                this.posts.push(newPost);
                this.title = "";
                this.body = "";
            },
        }
    }
</script>

<style>

* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

.app{
    padding: 20px;
}

.post{
    padding: 15px;
    border: 2px solid teal;
    margin-top: 15px;
}

form{
    display: flex;
    flex-direction: column;
}

.input{
    width: 100%;
    border: 1px solid teal;
    padding: 10px 15px;
    margin-top: 15px;
}

.btn{
    margin-top: 15px;
    align-self: flex-end;
    padding: 10px 15px;
    background: none;
    color: teal;
    border:1px solid teal;
}

</style>