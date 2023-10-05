<template lang="">
    <button class="btn">
        <slot></slot>
    </button>
</template>
<script>
export default {
    name: 'my-button'
}
</script>
<style scoped>
    
.btn{
    padding: 10px 15px;
    background: none;
    color: teal;
    border:1px solid teal;

    position: relative;
    transition: all .25s;
}
.btn span{
    position: relative;
    z-index: 2;
}
.btn:hover{
    color: #fff;
    background-color: teal;
    transition: all .25s;
}
</style>