<template lang="">
    <div>
        <div>
            <h2>Список постов</h2>
            <post-item v-for="post in posts" :key="post.id"
            :post="post"/>
        </div>
        
            
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