<template>
  <div>
    <welcome :welcomePage="websiteData.welcomePage"></welcome>
    <projects :projects="websiteData.projects"></projects>
    <about :about="websiteData.about"></about>
    <skillsets :skillsets="websiteData.skillsets"></skillsets>
    <contact :contact="websiteData.contactInfo"></contact>
  </div>
</template>


<script>
  import websiteData from '../../assets/website-data.json';
  import Welcome from './welcome';
  import Projects from './projects';
  import About from './about';
  import Skillsets from './skillsets';
  import Contact from './contact';

  export default {
    name: "main-page",
    data() {
      return {
        websiteData: websiteData,
        headerLinks : websiteData.headerLinks
      };
    },
    mounted() {
      console.log("Hello world!");
      console.log(this.websiteData);
    },
    components: {
      Welcome,
      Projects,
      About,
      Skillsets,
      Contact
    }
  }

</script>


<style>

</style>
