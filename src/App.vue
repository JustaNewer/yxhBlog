<template>
  <div id="app">
    <MyBlog />
  </div>
</template>

<script>
import MyBlog from './components/MyBlog.vue'

export default {
  name: 'App',
  components: {
    MyBlog
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

/* 重置一些基础样式 */
body {
  margin: 0;
  padding: 0;
}

* {
  box-sizing: border-box;
}
</style>
