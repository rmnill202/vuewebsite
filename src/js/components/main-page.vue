<template>
  <div>
    <h2>Header</h2>
    <h1>Welcome</h1>
    <h1>Projects</h1>
    <h1>About</h1>
    <h1>Skillsets</h1>
    <h1>Contact</h1>
  </div>
</template>


<script>
  import WebsiteData from '../../assets/website-data.json'

  export default {
    name: "main-page",
    data() {
      return {

      };
    },
    mounted() {
      console.log("Hello world!");
      console.log(WebsiteData);
    }
  }

</script>


<style>

</style>
