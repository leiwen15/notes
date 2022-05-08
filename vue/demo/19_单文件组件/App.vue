<template>
    <div id="root">
        <School/>
        <Student/>
    </div>
</template>

<script>
// 在脚手架中，.vue写也行，不写也行
    import School from './School.vue'
    import Student from './Student'
    export default {
        name:'App',
        components:{
            School,
            Student
        }
    }
</script>

<style>

</style>