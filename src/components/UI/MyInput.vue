<template lang="">
    <input :value="modelValue" @input="updateInput" class="input" type="text">
</template>
<script>
export default {
    name:'my-input',
    props: {
        modelValue: {String, Number}
    },
    methods: {
        updateInput(event){
            this.$emit('update:modalValue', event.target.value);
        }
    },
}
</script>
<style scoped>
.input{
    width: 90%;
    border: 1px solid teal;
    border-radius: 12px;
    padding: 10px 15px;
    margin-top: 15px;
    font-size: 16px;
    box-shadow: 0px 0px 4px 0px teal;
}
.input:focus{
    outline:none;
    border: 2px solid teal;
    border-radius: 14px;
}

</style>