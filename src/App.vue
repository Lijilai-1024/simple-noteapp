<template>
  <div id="app">
    <nav>
      <router-link to="/">Home</router-link> | 
      <router-link to="/register">注册</router-link> |
      <router-link to="/login">登录</router-link>
      
    </nav>
    <div></div>
    <router-view/>
  </div>
</template>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;
  font-size:20px;
  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
