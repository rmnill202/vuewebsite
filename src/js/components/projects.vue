<template>
  <div>
    <br> <!-- Section title -->
    <h1>Projects</h1>
    
    <!-- Container for the two columns displayed on larger screens -->
    <div class="hidden-sm-and-down larger"> 

      <!-- Display the projects in a grid -->
      <div class="gridSelection">
        <diamond-grid :elements="imgs" :pattern="[1,2]" 
            :selection="selected" @selected="updateSelected" 
            :width="120" :height="120" 
            class="hidden-sm-and-down"></diamond-grid>
      </div>
      
      <!-- Whatever project is selected, display a preview! -->
      <project-preview v-for="project in projects" :key="project.id" 
        :project="project.preview" class="gridPreview"></project-preview>
    </div>

    <!-- Container for accordion displayed on smaller screens -->
    <div class="hidden-md-and-up smaller">
      <v-expansion-panel>
        <v-expansion-panel-content v-for="i in imgs"  class="grey lighten-2">

          <!-- Title of the accordion -->
          <div slot="header">Title</div>

          <!-- Content -->
          <v-card>
            <v-card-text class="grey lighten-3">
              My content
            </v-card-text>
          </v-card>

        </v-expansion-panel-content>
      </v-expansion-panel>
    </div>

    <br><v-divider></v-divider>
  </div>
</template>

<script>
  import ProjectPreview from './util/project-preview.vue';
  import DiamondGrid from './util/diamond-grid.vue';

  export default {
    name: 'projects',
    props: ['projects'],
    components: {ProjectPreview, DiamondGrid},
    data() {
      return {
        selected: 1
      };
    },
    computed: {
      imgs() {
        return this.testArr(`gradient.png`);
      }
    },
    methods: {
      updateSelected(newIndex) {
        console.log(newIndex);
      },
      testArr(img) {
        const imgArr = [];
        for(let i = 0; i < 10; i++) {
          imgArr.push(require(`../../assets/${img}`));
        }
        return imgArr;
      }
    }
  };
</script>

<style>
  .larger {
    display: grid;
    grid-template-columns: 40% 20% 40%;
    margin-left: 5%;
    margin-right: 5%;
  }
  .smaller {
    margin-left: 5%;
    margin-right: 5%;
  }
  .gridSelection {
    grid-column: 1 / 2;
  }
  .gridPreview {
    grid-column: 3 / 4;
  }
</style>
