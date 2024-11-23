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
/* 全局样式 */
body {
  margin: 0;
  padding: 0;
  background-color: #1a1a1a !important;
  min-height: 100vh;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #ffffff;
  background-color: #1a1a1a;
  min-height: 100vh;
}

* {
  box-sizing: border-box;
}
</style>
