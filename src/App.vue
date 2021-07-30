<template>
  <img class="logo" src="../public/logo.png" alt="logo">
  <div id="nav">
    <router-link to="/">Catalogue</router-link>
    <router-link to="/about">About</router-link>
    <router-link to="/methodology">Methodology</router-link>
    <router-link to="/contact">Contact</router-link>
  </div>
  <router-view/>
</template>

<style>
.logo {
  float: left;
  max-width: 180px;
  margin: 10px 0 10px 10px;
}
.highlightLink a {
  color: #DC143C;
  padding: 4px;
}
.highlightLink a:hover {
  background: #DC143C;
  color: white;
  padding: 4px;
  border-radius: 4px
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #032b44;
}
#nav {
  padding: 30px;
}
#nav a {
  font-weight: bold;
  color: #032b44;
  margin: 25px 0;
  padding: 10px;
}
#nav a.router-link-exact-active {
  color: #fff;
  background: #DC143C;
  border-radius: 4px;
  text-align: center;
}
</style>
