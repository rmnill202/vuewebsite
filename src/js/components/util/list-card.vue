<template>
  <v-card :style="cardStyle" class="cardStyle">
    <!-- Title -->
    <v-card-title class="title">
      <!-- Optional Image or Icon; prefer images -->
      <img v-if="value.image" src="../../../assets/gradient.png" class="optionalImage" :style="imgStyle"/>
      <v-icon v-else-if="value.icon" class="optionalIcon">{{value.icon}}</v-icon>
      
      <div class="name"> {{value.name}} </div>
    </v-card-title>

    <!-- Description -->
    <v-card-text>
      <span>{{value.description}}</span>

      <div v-for="point in value.bulletPoints">
        {{point.text}}
      </div>
    </v-card-text>

    <!-- Bullet Points -->


  </v-card>
</template>

<script>
  export default {
    name: 'list-card',
    props: ['value', 'imgWidth', 'width'],
    data() {
      return {
      };
    },
    computed: {
      imgStyle() {
        if(this.imgWidth) {
          return {'width': this.imgWidth};
        }
      },
      cardStyle() {
        if(this.width) {
          return {'width': this.width};
        }
      }
    }
  }
</script>

<style>
  .name {
    width: 100%;
    text-align: center;
  }
  .optionalImage {
    -webkit-clip-path: polygon(50% 0%, 100% 50%, 50% 100%, 0% 50%);
    clip-path: polygon(50% 0%, 100% 50%, 50% 100%, 0% 50%);
    display: block;
    margin-left: auto;
    margin-right: auto;
    margin-bottom: 10px;
  }
  .optionalIcon {
    display: block;
    margin-left: auto;
    margin-right: auto;
    margin-bottom: 10px;
    font-size: 53px;
  }
  .cardStyle {
    margin-left: auto;
    margin-right: auto;
  }
</style>