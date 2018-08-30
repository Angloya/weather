<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Today's weather</router-link> |
      <router-link to="/london">London</router-link> |
      <router-link to="/moscow">Moscow</router-link> |
      <router-link to="/vladimir">Vladimir</router-link> |
      <router-link to="/newyork">New York</router-link>
    </div>
    <router-view/>
  </div>
</template>

<style>
@import url('https://fonts.googleapis.com/css?family=Poiret+One&subset=cyrillic,latin-ext');
#app {
  font-family: 'Poiret One', cursive;
  text-align: center;
  color: #2c3e50;
  background-image: url("./assets/background.jpg");
  background-size: cover;
  height: 100%;
  margin: 0;
  padding: 10px;
}
*{
  margin: 0;
  padding: 0;
}
h1 {
  padding-bottom: 10px;
  padding-top: 10px;
}
h2 {
  padding-bottom: 20px;
  padding-top: 5px;
}
h3 {
  padding: 5px;
}
a {
  text-decoration: none;
  color: black
}
#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
  font-size: 20px
}

#nav a.router-link-exact-active {
  color: #ffffff;
}

</style>
