<!-- 组件的结构 -->
<template>
    <div class="demo">
        <h2>学生姓名：{{name}}</h2>
        <h2>年龄：{{age}}</h2>
        <button @click="showName">点我显示学生名字</button>
    </div>
</template>

<!-- 组件交互相关的代码 -->
<script>
    export default {
        name: 'Student',
        data(){
            return {
                name: '小明',
                age: 15
            }    
        },
        methods: {
            showName(){
                alert(this.name)
            }
        },
    }
    // 默认暴露
    // export default school
</script>

<!-- 组件的样式 -->
<style>
    .demo{
        background-color:green
    }
</style>