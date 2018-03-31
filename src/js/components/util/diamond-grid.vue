<!-- Header goes here -->
<template>
  <div>
    <div v-for="(row, index) in renderRows" :key="row.id" :style="index === 0 ? topRowStyle : rowStyle" class="allRows">

      <!-- Element -->
      <img v-for="image in row" v-if="image" :src="image.element"
        :class="elementClass" :style="isSelected(image.index) ? selectedStyle : elementStyle" @click="selectElement(image.index)">

      <!-- Empty space -->
      <div v-else :class="emptyClass" :style="emptyStyle"/>
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
       * The index of the selected element, based on the array of elements passed into this component. If passed
       *   in, will be used to apply a "selected" styling to the element at the given index, and enables selection
       *   of elements. 
       */
      selection: {
        type: Number,
        required: false
      },
      /** 
       * An object that optionally defines styling to be applied to elements.
       */
      styling: {
        type: Object,
        required: false
      },
      /**
       * An array of visual elements to populate the grid with. Each element should be an object with a type
       *   parameter. Accepted types and formats are listed below:
       * Type: image
       *   src: Image URL
       *
       * Type: text
       *   text: The text that will be displayed.
       *   textStyle: The CSS styling that will be applied to the text.
       *   bgStyle: The CSS styling that will be applied to the background of the text.
       */
      elements: {
        type: Array,
        required: true
      },
      /** 
       * The width that will be applied to all visual elements, which must be consistent. If a width
       *   is not provided, then the width of the first image in the array of images will be used instead.
       */
      width: {
        type: Number,
        required: false,
        default: 200
      },
      /** 
       * The height that will be applied to all visual elements, which must be consistent. If a height
       *   is not provided, then the height of the first image in the array will be used instead.
       */
      height: {
        type: Number,
        required: false,
        default: 200
      },
      /**
       * The amount of spacing between rows of diamonds.
       */
      verticalSpacing: {
        type: Number,
        required: false,
        default: 5
      },
      /** 
       * The applied left and right margins for each image in the grid.
       */
      margins: {
        type: Number,
        required: false,
        default: 5
      },
      /**
       * If set to true, rows will be reversed when rendering.
       */
      flipVertical: {
        type: Boolean,
        required: false,
        default: false
      },
      /**
       * If set to true, each row will be reversed.
       */
      flipHorizontal: {
        type: Boolean,
        required: false,
        default: false
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
       * @return True if there is no element array, or if the array is empty.
       */
      noElements() {
        return !this.elements || this.elements.length < 1;
      },
      /** 
       * Based on the given list of elements and the pattern, construct an array of image rows,
       *  where the first row is what will be rendered at the top of the page. 
       */
      renderRows() {
        //Don't compute anything if we're missing the pattern or elements
        if(this.noPattern || this.noElements)
          return false;
        
        //Create an array of rows in order of the pattern. It'll be reversed later
        const rows = [];

        //Create rows until we run out of elements
        let elemIndex = 0, patternIndex = 0;

        while(elemIndex > -1) {
          const rowAndIndices = this.createRow(elemIndex, patternIndex);
          elemIndex = rowAndIndices.elemIndex;
          patternIndex = rowAndIndices.patternIndex;

          if(rowAndIndices.row)
            rows.push(this.flipHorizontal ? rowAndIndices.row.reverse() : rowAndIndices.row);
        }

        //Return there reversed order of elements by default, as we render top-down
        return rows.length > 0 ? (this.flipVertical ? rows : rows.reverse()) : undefined;
      },


      /** Row styling **/
      /****************/
      topRowStyle() {
        return { lineHeight: 0};
      },
      rowStyle() {
        return {marginTop:`-${(this.height / 2) - this.verticalSpacing}px`, lineHeight: 0};
      },

      /** Styling for elements & blank spaces **/
      /*****************************/
      allClass() {
        return ['diamond'];
      },
      allStyle() {
        return {'width': `${this.width}px`, 'height': `${this.height}px`, 
                'marginLeft': `${this.margins}px`, 'marginRight': `${this.margins}px`,
                'minWidth': `${this.width}px`};
      },

      /** Styling for all elements **/
      /*****************************/
      elementClass() {
        return this.allClass;
      },
      elementStyle() {
        return this.allStyle;
      },
      selectedStyle() {
        return Object.assign({}, this.elementStyle, {'opacity': '0.5'});
      },

      /** Styling empty spaces **/
      /*****************************/
      emptyClass() {
        return this.allClass;
      },
      emptyStyle() {
        return this.allStyle;
      }
    },
    methods: {
      /** 
       * Construct a row from the array of elements & pattern if possible.
       * @return An object containing the next element and pattern indices. If a row was created,
       *   then the row is also included in the object.
       */
      createRow(elemIndex, patternIndex) {
        //Setup some short-hand temp variables
        let iElm = this.elements[elemIndex] ? elemIndex : -1;
        const iPat = this.pattern[patternIndex] ? patternIndex : 0;

        //Check if we have any remaining elements
        if(iElm == -1) {
          return {elemIndex: -1, patternIndex: -1};
        }

        //Grab the next part of the pattern and initialize the new row
        const part = this.pattern[iPat];
        const row = [];

        //If the pattern part is an integer
        if(Number.isSafeInteger(part)) {

          //Grab the number of elements requested
          for(let toPush in this.elements.slice(iElm, iElm + part)) { 
            row.push({'index': iElm, 'element': this.elements[iElm++]})
          }

          //Fill the rest of the row with empty stuff if necessary
          if(row.length < part) { 
            for(let i = 0; i < (part - row.length); i++) { row.push(''); }
            iElm = -1;
          }
        }

        //If the pattern part is an array
        else if(Array.isArray(part)) {
          for(let el of part) {
            if(String(el).toLowerCase() === 'i') { //If element doesn't exist, set the element index to -1
              if(!this.elements[iElm]) {
                iElm = -1;
                row.push('');
              }else {
                row.push({'index': iElm, 'element': this.elements[iElm++]});
              }
            }else if(String(el).toLowerCase() === 'x') { //Otherwise add some space to the row
              row.push('');
            }
          }
        }
        
        //Return the row and updated indices
        return {'row': ((row.length > 0) ? row : undefined), 'elemIndex': iElm, 'patternIndex': iPat + 1};
      },
      /** 
       * Inform the parent context that the selection has changed.
       * @param index : The index of the new selection, which matches an index located in the elements array.
       */
      selectElement(index) {
        this.$emit('selected', index);
      },
      /** 
       * @return True if the element's index indicates that it has been selected.
       */
      isSelected(index) {
        return index === this.selection;
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

  .allRows {
    display: flex;
    justify-content: center;
    align-items: center;
  }
</style>
