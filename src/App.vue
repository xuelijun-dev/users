<template>
  <div id="app">
    <a href="#/home">主页</a>
    <a href="#/user">用户列表</a>
    <a href="#/student">学生列表</a>

    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>

<style>

</style>
