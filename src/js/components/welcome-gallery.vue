<template>
  <div>
    <div>
      <!-- Row -->
      <div style="line-height: 0">
        <img src="../../assets/test.jpg" class="diamond">
        <img src="../../assets/test.jpg" class="diamond">
        <img src="../../assets/test.jpg" class="diamond">
      </div>

      <!-- Row -->
      <div class="diamondBelow">
        <img src="../../assets/test.jpg" class="diamond">
        <img src="../../assets/test.jpg" class="diamond">
      </div>

      <!-- Row -->
      <div class="diamondBelow">
        <img src="../../assets/test.jpg" class="diamond">
      </div>

      <!-- Row -->
      <div class="diamondBelow">
        <img src="../../assets/test.jpg" class="diamond">
        <img src="../../assets/test.jpg" class="diamond">
      </div>

      <!-- Row -->
      <div class="diamondBelow">
        <img src="../../assets/test.jpg" class="diamond">
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'welcome-gallery',
    props: ['left', 'right', 'center'],
    data() {

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
