<template>
  <div>
    <!-- Website title -->
    <v-divider></v-divider>
    <br>
    <h1>{{title}}</h1>

    <!-- Image gallery -->
    <welcome-gallery :left="left" :right="right" :center="center" style="filter: drop-shadow(0px 3px 2px #000000)"></welcome-gallery>

    <!-- Description -->
    <div class="description title">{{description}}</div>

    <!-- Resume link -->
    <div class="resume title"><a href="https://people.rit.edu/rmn6979/2018_Robert_Nill_Software_Engineer_Resume.pdf">Download my resume here - <i class="fas fa-file-alt"></i></a></div>

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
        recentEvents: this.welcomePage.recentEvents,
        left: this.welcomePage.previewImages.left,
        right: this.welcomePage.previewImages.right,
        center: this.welcomePage.previewImages.center,
      }
    },
  };
</script>

<style>
  .resume {
    margin: 10px 20% 30px 20%;
  }
  .description {
    margin: 30px 20% 10px 20%;
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
