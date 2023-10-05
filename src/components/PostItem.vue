<template lang="">
    <div class="blog_post">
        <div class="post">
            <div>
                <div><h2>Название: {{ post.title }}</h2></div>
                <div><p>{{ post.body }}</p></div>
            </div>
            <div class="post_btn">
                <my-button
                 @click="$emit('remove', post)">
                Удалить</my-button>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    props:{
        post:{
            type: Object,
            required: true
        }
    }
}
</script>
<style scoped>
.blog_post{
    background: #fff;
    border-radius: 10px;
    box-shadow: 1px 1px 1rem rgba(0, 0, 0, 0.3);
}
.post{
    padding: 15px;
    border: 2px solid teal;
    margin-top: 15px;
    display: flex;
    align-items: center;
    justify-content: space-between;
}   
h3 {
  margin: 0 0 0.5rem 0;
  color: #776868;
  font-size: 1.25rem;
}
h2 {
  margin: 0 0 1rem 0;
  font-size: 1.5rem;
  letter-spacing: 0.5px;
  color: #333;
}
p {
  margin: 0 0 4.5rem 0;
  font-size: 1.5rem;
  line-height: 1.45;
  color: #333;
}
.post_btn{
    align-self:flex-end;
}
</style>