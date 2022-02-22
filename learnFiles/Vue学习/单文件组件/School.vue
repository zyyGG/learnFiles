<template>
    <div class="demo">
        <p></p>
        <p>学校名称：{{name}}</p>
        <p>学校地址：{{address}}</p>
        <button @click="showName">显示学校名字</button>
        <p>Hello</p>
    </div>
</template>

<script>
    //默认暴露  import ??? form ???
    //export default school
    export default {
        name:"School",
        data(){
            return {
                name:"ABC",
                address:"DEF",
            }
        },
        methods:{
            showName(){
                console.log(this.name);
            }
        }
    }
    
</script>

<style>
    /* 组件的样式 */
    .demo{
        background-color:red;
    }
</style>