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
      this.$message('Toast from element-ui')
    }
  }
}
</script>

<style>

</style>
