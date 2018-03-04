<template>
  <div>
    <diamond-grid :images="images" :pattern="altPattern" width=120 height=120 
                  flip-horizontal=true class="hidden-md-and-up altTop"></diamond-grid>
    <div style="display: flex; justify-content: center">
      <diamond-grid :images="images" :pattern="pattern" width=120 height=120 
                    flip-horizontal=true class="hidden-sm-and-down"></diamond-grid>
      <img src="../../assets/test.png" class="center">
      <diamond-grid :images="images" :pattern="pattern" width=120 height=120 
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
        images: [require("../../assets/test.png"), require("../../assets/test.png"), 
                require("../../assets/test.png"), require("../../assets/test.png")],
        altPattern: [["i", "x", "i"], 2],
        altImages: [require("../../assets/test.png"), require("../../assets/test.png")]
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
