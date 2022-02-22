<template>
    <div>
        <p>学生名称：{{name}}</p>
        <p>年龄：{{age}}
    </div>
</template>

<script>
export default {
    name:"Student",
    data(){
        return {
            name:"张三",
            age:18,
        }
    }
}
</script>

<style>
    
</style>