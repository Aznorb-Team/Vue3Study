<template lang="">
    <div class="dialog" v-if="show" @click.stop="hideDialog">
        <div @click.stop class="dialog_content">
            <slot></slot>
        </div>
    </div>
</template>
<script>
import toogleMixin from '@/mixins/toobleMixin'

export default {
    name:'my-dialog',
    mixins: [toogleMixin]
}
</script>
<style>
    .dialog{
        top: 0;
        bottom: 0;
        right: 0;
        left: 0;
        background: rgba(0,0,0,0.5);
        position: fixed;
        display: flex;
        z-index: 1000;
    }
    .dialog_content{
        margin: auto;
        background: white;
        border-radius: 12px;
        min-height: 50px;
        min-width: 300px;
        padding: 20px;
        border: 3px solid teal;
        
    }
</style>