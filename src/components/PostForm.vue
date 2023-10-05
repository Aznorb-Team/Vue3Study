<template lang="">
    <form @submit.prevent>
                <h4>Создание поста</h4>
                <my-input v-bind:value="post.title" @input="post.title = $event.target.value" placeholder="Название"></my-input>
                <my-input v-bind:value="post.body" @input="post.body = $event.target.value" placeholder="Описание"></my-input>
                <my-button @click="createPost"
                style="align-self:flex-end; margin-top: 15px;">Создать</my-button>
            </form>
</template>
<script>
export default {
    data(){
        return{
            post:{
                title: "",
                body: "",
            }
        }
    },
    methods: {
        createPost(){
                
                    this.post.id = Date.now();
                    this.$emit('create', this.post);
                    this.post = {
                        title: '',
                        body: ''
                    }
                
            },
    },
}
</script>
<style scoped>
    form{
    display: flex;
    flex-direction: column;
}
</style>