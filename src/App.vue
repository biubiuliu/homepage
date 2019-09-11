<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  min-width: 900px;
}
html {font-size: 62.5%!important; /* 10÷16=62.5% */}
@media only screen and (min-width: 481px){
    html {
        font-size: 94%!important; /* 15.04÷16=94% */
    }
}
@media only screen and (min-width: 561px){
    html {
        font-size: 109%!important; /* 17.44÷16=109% */
    }
}
@media only screen and (min-width: 641px){
    html {
        font-size: 125%!important; /* 20÷16=125% */
    }
}
</style>
