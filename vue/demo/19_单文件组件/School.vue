<!-- 组件的结构 -->
<template>
    <div class="demo">
        <h2>学校名称：{{schoolName}}</h2>
        <h2>学校地址：{{address}}</h2>
        <button @click="showName">点我显示学校名字</button>
    </div>
</template>

<!-- 组件交互相关的代码 -->
<script>
    export default {
        name: 'School',
        data(){
            return {
                schoolName: '三中',
                address: '松露'
            }    
        },
        methods: {
            showName(){
                alert(this.schoolName)
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