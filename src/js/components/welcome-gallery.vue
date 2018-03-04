<template>
  <div>
    <diamond-grid :images="altImages" :pattern="altPattern" :width="size" :height="size"
                  class="hidden-md-and-up altTop"></diamond-grid>
    <div style="display: flex; justify-content: center">
      <diamond-grid :images="leftImages" :pattern="pattern" :width="size" :height="size"
                    flip-horizontal=true class="hidden-sm-and-down"></diamond-grid>
      <img :src="centerImage" class="center">
      <diamond-grid :images="rightImages" :pattern="pattern" :width="size" :height="size"
                    class="hidden-sm-and-down"></diamond-grid>
    </div>
  </div>
</template>

<script>
  import DiamondGrid from './util/diamond-grid.vue';

  export default {
    name: 'welcome-gallery',
    props: ['left', 'right', 'center'],
    components: {DiamondGrid},
    data() {
      return {
        pattern: [["i", "x"], 1, 2],
        altPattern: [["i", "x", "i"], 2],
        size: 120
      }
    },
    computed: {
      leftImages() {
        return this.imageArr(this.left);
      },
      rightImages() {
        return this.imageArr(this.right);
      },
      centerImage() {
        return require(`../../assets/${this.center}`);
      },
      altImages() {
        return this.imageArr(this.left);
      }
    },
    methods: {
      /** 
       * Construct an array of images. The require call is necessary to load the image.
       * @param source : The source array of images, which have not yet been required.
       * @return The array of image sources that can now be bound using v-bind!
       */
      imageArr(source) {
        const imgArr = [];
        for(let img of source) {
          imgArr.push(require(`../../assets/${img}`));
        }
        return imgArr;
      }
    }
  }
</script>

<style>
  .center {
    -webkit-clip-path: polygon(50% 0%, 100% 50%, 50% 100%, 0% 50%);
    clip-path: polygon(50% 0%, 100% 50%, 50% 100%, 0% 50%);
    display: inline-block;
    min-width: 250px;
    min-height: 250px;
    width: 250px;
    height: 250px;
    flex-grow: 0;
    margin: 0px 60px 0px 60px;
  }

  .altTop {
    margin-bottom: -120px;
  }
</style>
