<template>
  <div>
    <div>
      <diamond-grid :images="images" :pattern="pattern"></diamond-grid>
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
        pattern: [1, 2, ["i", "X", "i"], 2],
        images: [require("../../assets/test.jpg"), require("../../assets/test.jpg"), require("../../assets/test.jpg"),
        require("../../assets/test.jpg"), require("../../assets/test.jpg"), require("../../assets/test.jpg"),
        require("../../assets/test.jpg"),require("../../assets/test.jpg")],
      }
    }
  }
</script>

<style>
  .diamond {
    -webkit-clip-path: polygon(50% 0%, 100% 50%, 50% 100%, 0% 50%);
    clip-path: polygon(50% 0%, 100% 50%, 50% 100%, 0% 50%);
    width: 200px;
    height: 200px;
    display: inline-block;
  }
  .diamondBelow {
    /*position: relative;*/
    margin-top:-95px;
    line-height: 0;
  }
</style>
