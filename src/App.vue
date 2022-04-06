<template>
  <header></header>
  <router-view/>
</template>

<style lang="scss">
@font-face {
  font-family: Roboto;
  font-style: normal;
  font-display: swap;
  font-weight: 10;
  src:url('@/assets/fonts/Roboto/Roboto-Regular.ttf');
  src: url('~assets/fonts/Roboto/Roboto-Regular.ttf');
}
header{
  width: 1440px;
  height: 48px;
  left: 0px;
  top: 0px;
  background: #11B980;
  margin-bottom: 69px;
}
#app {
  font-family: 'Roboto';
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
@import'~bootstrap/dist/css/bootstrap.css'
</style>
