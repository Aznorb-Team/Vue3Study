<template lang="">
    <div>
        <div v-if="posts.length > 0">
            <h2>Список постов</h2>
            <post-item 
            v-for="post in posts" 
            :key="post.id"
            :post="post"
            @remove="$emit('remove', post)"/>
        </div>
        <h2 v-else style="color:red;">Список постов пуст!</h2>
            
    </div>
</template>
<script>
import PostItem from "@/components/PostItem.vue";
export default {
    components: {PostItem},
    props: {
        posts:{
            type : Array,
            required: true
        }
    }
}
</script>
<style scoped>


</style>