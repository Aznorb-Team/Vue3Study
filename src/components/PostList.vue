<template lang="">
    <div>
        <div v-if="posts.length > 0" class="post_list">
            <h2>Список постов</h2>
                <ul class="tilesWrap">
                    <!-- <transition-group tag="ul" class="tilesWrap" name="postlist"> -->
                        <post-item 
                        v-for="post in posts" 
                        :post="post"
                        :key="post.id"
                        @remove="removeMethod">
                        </post-item>
                    <!-- </transition-group> -->
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
    },
    methods: {
        removeMethod(p){
            this.$emit('remove', p);
        }
    },
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

/* .postlist-item {
  display: inline-block;
  margin-right: 10px;
}
.postlist-enter-active,
.postlist-leave-active {
  transition: all 0.4s ease;
}
.postlist-enter-from,
.postlist-leave-to {
  opacity: 0;
  transform: translateX(-130px);
}
.postlist-move {
  transition: transform 0.8s ease;
} */
</style>