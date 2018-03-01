<!-- Header goes here -->
<template>
  <div>
    <!--
    //Render the top row
    //Render the remaining rows using a v-for loop
    -->
  </div>
</template>

<script>
  export default {
    name: 'diamond-grid',
    props: ['pattern', 'offsets', 'images', 'spacing', 'size', 'startFrom'],
    data() {
      return {

      }
    },
    computed: {
      rows() {
        //First, let's take the length of images and fit the pattern to that length
          //ex: 5, pattern is 1-2. We get 1-2-1-2 (1, 23, 4, 5x) (x is added, but is invisible)
        //Now, let's reverse the pattern order, and therefore the indices

        //We'll return [ [5,x],[4,3],[2,1] ];
      },
      topRow() {

      },
      remainingRows() {

      },
      canRender() {

      }
    }
  }
</script>

<style>
  .diamond {
    -webkit-clip-path: polygon(50% 0%, 100% 50%, 50% 100%, 0% 50%);
    clip-path: polygon(50% 0%, 100% 50%, 50% 100%, 0% 50%);
    display: inline-block;
  }
</style>
