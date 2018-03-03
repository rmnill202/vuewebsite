<!-- Header goes here -->
<template>
  <div>
    <!-- Start off by rendering the top row -->
    <div v-if="topRow" style="line-height: 0;">
      <img v-for="image in topRow" :key="image.id" :src="image" :class="imgClass">
    </div>

    <!-- Now render the rest of the content, if it exists -->
    <div v-for="row in bottomRows" :key="row.id" style="margin-top:-95px; line-height: 0;">
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
        type: Array,
        required: true
      },
      /**
       * An array of image URLs to populate the grid with.
       */
      images: {
        type: Array,
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
       * @return True if there is no pattern array, or if the pattern object is empty.
       */
      noPattern() {
        return !this.pattern || this.pattern.length < 1;
      },
      /** 
       * @return True if there is no image array, or if the array is empty.
       */
      noImages() {
        return !this.images || this.images.length < 1;
      },
      /** 
       * Based on the given list of images and the pattern, construct an array of image rows,
       *  where the first row is what will be rendered at the top of the page. 
       */
      renderRows() {
        //Don't compute anything if we're missing the pattern or images
        if(this.noPattern || this.noImages)
          return false;
        
        //Create an array of rows in order of the pattern. It'll be reversed later
        const rows = [];

        //Create rows until we run out of images
        let imageIndex = 0, patternIndex = 0;

        while(imageIndex > -1) {
          const rowAndIndices = this.createRow(imageIndex, patternIndex);
          imageIndex = rowAndIndices.imageIndex;
          patternIndex = rowAndIndices.patternIndex;

          if(rowAndIndices.row)
            rows.push(rowAndIndices.row);

          console.log(rowAndIndices);
        }

        //Return there reversed order of images by default, as we render top-down
        return rows.length > 0 ? rows.reverse() : undefined;
      },
      /** 
       * @return Rows in order of how they should be rendered, excluding the topmost row.
       */
      bottomRows() {
        return this.renderRows ? this.renderRows.slice(1, this.renderRows.length) : [];
      },
      /** 
       * @return The first row that should be rendered.
       */
      topRow() {
        return this.renderRows ? this.renderRows[0] : [];
      },
      /** 
       * @return The CSS classes that should be applied to all images.
       */
      imgClass() {
        return ['diamond'];
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
        //Setup some short-hand temp variables
        let iImg = this.images[imageIndex] ? imageIndex : -1;
        const iPat = this.pattern[patternIndex] ? patternIndex : 0;

        //Check if we have any remaining images
        if(iImg == -1)
          return {imageIndex: -1, patternIndex: -1}

        //Grab the next part of the pattern and initialize the new row
        const part = this.pattern[iPat];
        const row = [];

        // //If the pattern part is an integer
        if(Number.isSafeInteger(part)) {
          //Grab the number of images requested
          row.push( ...(this.images.slice(iImg, iImg + part)) );

          
          if(row.length < part) {
            //Fill the rest of the row with empty stuff
            for(let i = 0; i < (part - row.length); i++) {
              row.push("");
            }
            iImg = -1;
          }
          else
            iImg += part;
        }

        //If the pattern part is an array
        else if(Array.isArray(part)) {
          for(let el of part) {
            if(el === "i") { //If image doesn't exist, set iImg to -1 and break
              if(!this.images[iImg]) {
                iImg = -1;
                row.push("");
              }else {
                row.push(this.images[iImg++]);
              }
            }else if(el === "X") { //Otherwise add some space to the row
              row.push("");
            }
          }
        }
        
        //Return the row and updated indices
        return {'row': ((row.length > 0) ? row : undefined), 'imageIndex': iImg, 'patternIndex': iPat + 1};
      }
    }
  }
</script>

<style>
  .diamond {
    -webkit-clip-path: polygon(50% 0%, 100% 50%, 50% 100%, 0% 50%);
    clip-path: polygon(50% 0%, 100% 50%, 50% 100%, 0% 50%);
    display: inline-block;

    width: 200px;
    height: 200px;
  }
</style>
