<!-- Header goes here -->
<template>
  <div>
    <!-- Start off by rendering the top row -->
    <div v-if="topRow">
      <img v-for="image in topRow" :key="image.id" :src="image">
    </div>

    <!-- Now render the rest of the content, if it exists -->
    <div v-for="row in bottomRows" :key="row.id">
      <img v-for="image in row" :key="image.id" :src="image" :class="imgClass">
    </div>
  </div>
</template>

<script>
  export default {
    name: 'diamond-grid',
    props: {
      /**
       * Defines the number of images/visual elements used for [n] rows, where [n] is the size of the array passed
       *   in as the pattern. The pattern will be repeated as many times as necessary for all images passed in to be
       *   displayed.
       *
       *  By default, patterns begin to fill the grid from the bottom left.
       *
       *  A pattern is contained within an object/array, and contains one of two types of pattern elements:
       *    1. Integers that define the number of images each row has.
       *    2. Arrays containing the characters 'i' or 'x', which represent 'image' and 'empty space' respectively.
       *
       *  An example containing both, and creates a grid of diamonds with an empty center.
       *  [ 1, 2, [i, x, i], 2, 1 ]
       */
      pattern: {
        type: Object,
        required: true
      },
      /**
       * An array of image URLs to populate the grid with.
       */
      images: {
        type: Object,
        required: true
      },
      /**
       * TODO: 
       */
      offsets: {},
      /**
       * TODO:
       */
      spacing: {},
      /**
       * Defines what vertical direction new rows are added from.
       */
      rowStart: {
        type: String,
        required: false,
        default: 'bottom'
      },
      /**
       * What side each row should start populating with images. Either 'left' or 'right'.
       */
      columnStart: {
        type: String,
        required: false,
        default: 'left'
      }
    },
    data() {
      return {}
    },
    computed: {
      /** 
       * Based on the given list of images and the pattern, construct an array of image rows,
       *  where the first row is what will be rendered at the top of the page. 
       */
      rows() {
        if(!this.pattern || (this.images instanceof Array))
          return false;
        
        //Create an array of rows in order of the pattern. It'll be reversed later
        const rows = [];

        //Create rows until we run out of images
        let imageIndex = 0, patternIndex = 0;
        while(imageIndex > -1) {
          const rowAndIndices = createRow(imageIndex, patternIndex);
          imageIndex = rowAndIndices.imageIndex;
          patternIndex = rowAndIndices.patternIndex;

          if(rowAndIndices.row)
            rows.push(rowAndIndices.row);
        }

        return rows.length > 0 ? rows.reverse() : undefined;
      },
      /** 
       * @return Rows in order of how they should be rendered, excluding the topmost row.
       */
      bottomRows() {
        return rows ? rows.slice(1, rows.length) : [];
      },
      /** 
       * @return The first row that should be rendered.
       */
      topRow() {
        return rows ? rows[0] : [];
      },
      /** 
       * @return The CSS classes that should be applied to all images.
       */
      imgClass() {
        return {};
      },
      /** 
       * @return Any CSS styling that should be applied to all images. Should be useful
       *   for any dynamic styles.
       */
      imgStyle() {
        return {};
      }
    },
    methods: {
      createRow(imageIndex, patternIndex) {
        const pattern = this.pattern[patternIndex];

        //Integer case

        //Array case

        //Undefined case

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
