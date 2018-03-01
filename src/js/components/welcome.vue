<template>
  <div>
    <!-- Website title -->
    <v-divider></v-divider>
    <h1>{{title}}</h1>

    <!-- Image gallery -->
    <welcome-gallery></welcome-gallery>

    <!-- Description -->
    <div class="description">{{description}}</div>

    <!-- Recent events -->
    <v-container grid-list-md>
      <div class="recentEvents" v-for="event in recentEvents">
        <v-flex class="eventLeft">Left</v-flex>
        <v-flex class="eventRight">Right</v-flex>
      </div>
    </v-container>

    <v-divider></v-divider>
  </div>
</template>

<script>
  import WelcomeGallery from './welcome-gallery.vue';

  export default {
    name: 'welcome',
    props: ['welcomePage'],
    components: {WelcomeGallery},
    data() {
      return {
        title: this.welcomePage.websiteName,
        description: this.welcomePage.description,
        recentEvents: this.welcomePage.recentEvents
      };
    },
  };
</script>

<style>
  .description {
    margin-left: 20%;
    margin-right: 20%;
  }
  .recentEvents {
    margin-left: 20%;
    margin-right: 20%;

  }
  .eventLeft {
    text-align: left;
  }
  .eventRight {
    text-align: right;
  }
</style>
