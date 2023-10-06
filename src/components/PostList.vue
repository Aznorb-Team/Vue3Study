<template lang="">
    <div>
        <div v-if="posts.length > 0" class="post_list">
            <h2>Список постов</h2>
            <ul class="tilesWrap">
                <post-item 
                v-for="post in posts" 
                :key="post.id"
                :post="post"
                @remove="$emit('remove', post)"/>
            </ul>
            
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
.post_list{
    /* border: 2px solid teal; */
    padding: 10px;
    text-align: center;
}
.tilesWrap {
	padding: 0;
	margin: 20px auto;
	list-style: none;
	text-align: center;
}
</style>