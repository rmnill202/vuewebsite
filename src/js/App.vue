<template>
  <div id="app">
    <head> <!-- Include material icons -->
      <link
        href='https://fonts.googleapis.com/css?family=Roboto:300,400,500,700|Material+Icons'
            rel="stylesheet">
    </head>
    <body>
      <v-app> <!-- Required for Vuetify to work correctly -->
        <router-view></router-view>
      </v-app>
    </body>
  </div>
</template>

<script>
  export default {
    name: 'app',
  };
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
