<template>
  <div>
    <br> <!-- Section title -->
    <h1>Projects</h1>
    
    <!-- Container for the two columns displayed on larger screens -->
    <div class="hidden-sm-and-down larger"> 

      <!-- Display the projects in a grid -->
      <div class="gridSelection">
        <diamond-grid :elements="imgs" :pattern="[1,2]" 
            :selection="selectedIndex" @selected="updateSelected" 
            :width="120" :height="120" 
            class="hidden-sm-and-down"></diamond-grid>
      </div>
      
      <!-- Whatever project is selected, display a preview! -->
      <project-preview v-if="selected" :project="selected" :name="selected.name" class="gridPreview"/>
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
        selectedIndex: -1
      };
    },
    computed: {
      imgs() {
        return this.testArr(`gradient.png`);
      },
      projectData() {
        const projectData = [];

        //Loop through each project and gather the following data:
        for(let i = 0; i < this.projects.length; i++) {
          // console.log("Projects");
          // console.log(this.projects);
          // console.log(proj);
          const proj = this.projects[i];
          projectData.push({
            'name': proj.preview.name, //Name
            'description': proj.preview.description, //Description
            'image': this.getImage(proj.preview.images) //First image OR default image
          });
        }

        return projectData;
      },
      selected() {
        console.log(this.projectData[this.selectedIndex]);
        return this.projectData[this.selectedIndex];
        // return false;
      }
    },
    methods: {
      updateSelected(newIndex) {
        this.selectedIndex = (newIndex === this.selectedIndex) ? -1 : newIndex;
      },
      testArr(img) {
        const imgArr = [];
        for(let i = 0; i < this.projectData.length; i++) {
          imgArr.push(require(`../../assets/${img}`));
        }
        return imgArr;
      },
      getImage(images) {
        if(!images || !images.length) {
          return require(`../../assets/${images[0]}`);
        } else {
          return require(`../../assets/gradient.png`);
        }
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
