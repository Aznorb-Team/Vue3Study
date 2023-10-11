<template lang="">
    <div class="navbar">
        <div @click="$router.push('/')">Vue 3</div>
        <div class="navbar_btn">
            <my-button @click="$router.push('/posts')" style="margin-right: 20px;">Посты</my-button>
            <my-button @click="$router.push('/about')">О сайте</my-button>
        </div>
    </div>
</template>
<script>
export default {
    name:'nav-bar'
}
</script>
<style scoped>
    .navbar{
        height: 50px;
        background-color: white;
        box-shadow: 2px 2px 4px gray;
        display: flex;
        align-items: center;
        padding: 0 15px;
    }
    .navbar_btn{
        margin-left: auto;
    }
</style>