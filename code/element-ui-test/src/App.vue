<template>
  <div id="app">
    <el-button @click='click'>点我</el-button>
  </div>
</template>

<script>

export default {
  name: 'App',
  methods:{
    click(){
      this.$message.success('Toast from element-ui')
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
