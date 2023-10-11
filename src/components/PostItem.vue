<template>
    <!-- <div class="blog_post">
        <div class="post">
            <div>
                <div><h2>{{ post.title }}</h2></div>
                <div><p>{{ post.body }}</p></div>
            </div>
            <div class="post_btn">
                <my-button
                 @click="$emit('remove', post)">
                Удалить</my-button>
            </div>
        </div>
    </div> -->
    <li>
        <!-- <h2>{{post.id}}</h2> -->
		<h3>{{post.id}}) {{post.title}}</h3>
		<p>
			{{post.body}}
		</p>
		<div class="post_delete">
            <my-button
                 @click="$router.push('/posts/'+ post.id)"
                 style="align-self:flex-end; margin-right: 20px;">
                Открыть</my-button>
            <my-button
                 @click="$emit('remove', post)"
                 style="align-self:flex-end;">
                Удалить</my-button>
        </div>
        
    </li>
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
/* .blog_post{
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
} */
li {
	display: inline-block;
	width: 20%;
	min-width: 330px;
	max-width: 360px;
    min-height: 400px;
	padding: 20px 20px 20px;
	vertical-align: top;
	margin: 10px;
	font-family: 'helvetica', san-serif;
	background: white;
	border: 1px solid teal;
	text-align: left;
    position: relative;
}
li h2 {
	font-size: 114px;
	margin: 0;
	opacity: 0.2;
    position: absolute;
    right: 10%;
    top: 10%;
    float: left;
    text-align: right;
	transition: all 0.3s ease-in-out;
}
li h3 {
	font-size: 20px;
	color: black;
	margin-bottom: 5px;
}
li p {
	font-size: 16px;
	line-height: 18px;
	color: black;
	margin-top: 5px;
    margin-bottom: 15px;
}
li:hover h2 {
    transform: translate(0%, -40%);
	opacity: 0.6;
}
.post_delete{
    position: absolute;
    right: 5%;
    bottom: 5%;
}
</style>