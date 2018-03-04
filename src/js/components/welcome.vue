<template>
  <div>
    <!-- Website title -->
    <v-divider></v-divider>
    <br>
    <h1>{{title}}</h1>

    <!-- Image gallery -->
    <welcome-gallery></welcome-gallery>

    <!-- Description -->
    <div class="description title">{{description}}</div>

    <!-- Recent events -->
    <div class="recentEvents" v-for="event in recentEvents" :key="event.id">
      <div class="eventLeft">{{event.description}}</div>
      <div class="eventRight">{{event.dateText}}</div>
    </div>

    <br>
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
    margin-top: 30px;
    margin-bottom: 30px;
    margin-left: 20%;
    margin-right: 20%;
  }
  .recentEvents {
    margin-left: 20%;
    margin-right: 20%;
    display: flex;
    justify-content: space-between;
  }
  .eventLeft {
    text-align: left;
    font-weight: bold;
  }
  .eventRight {
    text-align: right;
  }
  /** CSS for smaller stuff */
  @media screen and (max-width:960px) {
    .description {
      margin-top: 30px;
      margin-bottom: 0px;
      margin-left: 5%;
      margin-right: 5%;
    }
    .recentEvents {
      display: inline;
      margin-left: 20%;
      margin-right: 20%;
    }
    .eventLeft, .eventRight {
      text-align: center;
      margin-left: 5%;
      margin-right: 5%;
    }
  }
</style>
