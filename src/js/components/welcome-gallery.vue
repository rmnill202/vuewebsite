<template>
  <div>
    <div>
      <diamond-grid :images="images" :pattern="pattern" width=200 height=200></diamond-grid>
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
        images: [require("../../assets/test.png"), require("../../assets/test.png"), require("../../assets/test.png"),
          require("../../assets/test.png"), require("../../assets/test.png"), require("../../assets/test.png"), require("../../assets/test.png")],
      }
    }
  }
</script>

<style>

</style>
