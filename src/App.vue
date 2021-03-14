<template>
  <div id="app">
    <div id="nav" class="">
      <router-link to="/">Home</router-link> |
      <router-link to="/regiones">Pokedex</router-link>
    </div>
    <router-view/>
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  box-sizing: border-box;
  margin: 0;

}

#nav {
  padding: 30px;
  display: flex;
  flex-flow: row;
  border-bottom: 1px solid #333;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
  margin: 0 2rem;
  text-decoration: none;
  transition: all .2s;
}

#nav a:hover {
  transform: scale(1.2);
}

#nav a.router-link-exact-active {
  color: #e22a2a;
}
</style>
