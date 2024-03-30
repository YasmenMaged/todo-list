<template>
  <div id="app" class="container">
    <img alt="Vue logo" src="./assets/logo.png" class="logo">
    <nav>
      <router-link to="/">Home</router-link> |
      <router-link to="/todo">Todo</router-link>
    </nav>
    <router-view/>
  </div>
</template>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Madimi+One&display=swap');

*{
  box-sizing: border-box;
  font-family: "Madimi One", sans-serif;
}
.container{
  max-width: 600px;
  margin: 0 auto;
}
#app {
  font-family: "Madimi One", sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
.logo{
  display: block;
  margin: 20px auto;
  height: 200px;
}

nav {
  padding: 30px;
  font-size: 30px;

  a {
    font-weight: bold;
    color: #673F69;
    text-decoration: none;
    &.router-link-exact-active {
      color: #D74B76;
    }
  }
}
</style>
