<template>
  <div class="home"> 
    <a href="https://nimo.sjtu.edu.cn" target="_blank">
      <img alt="Vue logo" src="../assets/logo.png">
    </a>
    <Introduction msg="Simple-Noteapp"/>
  </div>
</template>

<style>
img{
  width:100px;
  height:100px;
}
</style>

<script>
// @ is an alias to /src
import Introduction from '@/components/Introduction.vue'

export default {
  name: 'HomeView',
  components: {
    Introduction
  }
}
</script>
