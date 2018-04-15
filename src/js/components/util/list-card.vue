<template>
  <v-card :style="cardStyle" class="cardStyle">

    <!-- Title -->
    <v-card-title class="title">
      <!-- Optional Image or Icon; prefer images -->
      <div class="imgcontainer">
        <img v-if="value.image" :src="getSrc(value.image)" class="optionalImage" :style="imgStyle"/>
        <v-icon v-if="value.icon && value.image" class="iconWithImage">{{value.icon}}</v-icon>
        <v-icon v-else-if="value.icon" class="optionalIcon">{{value.icon}}</v-icon>
      </div>
      
      
      <div class="name"> {{value.name}} </div>
    </v-card-title>

    <!-- Description -->
    <v-card-text style="padding-top: 0">
      <span>{{value.description}}</span>

      <!-- Bullet Points -->
      <div v-for="point in value.bulletPoints">
        {{point.text}}
      </div>

      <!-- Gallery -->
      <v-container v-if="value.gallery" grid-list-xs style="margin-top: 16px">
        <v-layout row wrap>
          <v-flex style="padding: 2px" v-for="item in value.gallery">
            <v-card flat>
               <v-tooltip bottom>
                <img :src="getSrc(item)" slot="activator" class="galleryImage" :style="galleryStyle"/>
                <span>{{item.text}}</span> <!-- Tooltip text -->
              </v-tooltip>
            </v-card>
          </v-flex>
        </v-layout>
      </v-container>
    </v-card-text>

  </v-card>
</template>

<script>
  export default {
    name: 'list-card',
    props: ['value', 'imgWidth', 'width', 'galleryWidth'],
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
      },
      galleryStyle() {
        return this.galleryWidth ? {'width': this.galleryWidth} : this.imgStyle;
      }
    },
    methods: {
      getSrc(item) {
        return require(`../../../assets/${item.img}`);
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
  }
  .optionalIcon {
    display: block;
    font-size: 53px;
  }
  .cardStyle {
    margin-left: auto;
    margin-right: auto;
  }
  .imgcontainer {
    display: block;
    margin-left: auto;
    margin-right: auto;
    margin-bottom: 10px;
  }
  .iconWithImage {
    display: block;
    font-size: 53px;
    position: absolute;
    transform: translate(-50%, -106%);
  }
  .galleryImage {
    display: block;
    margin-left: auto;
    margin-right: auto;
    width: 100%;
    height: 100%;
  }
</style>