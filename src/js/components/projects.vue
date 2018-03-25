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
      <project-preview v-if="selected" :project="selected" :mediaHeight="'200px'" class="gridPreview"/>
    </div>

    <!-- Container for accordion displayed on smaller screens -->
    <div class="hidden-md-and-up smaller">
      <v-container fluid grid-list-lg>
        <v-layout row wrap>
          
          <v-flex v-for="(project, index) in projectData" xs12>
            <project-preview :project="projectData[projectData.length -1 -index]" :mediaHeight="'100px'"/>
          </v-flex>

        </v-layout>
      </v-container>
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
        return this.projectData[this.selectedIndex];
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
          return require(`../../assets/gradient.png`);
        } else {
          return require(`../../assets/${images[0].img}`);
        }
      },
      gridSize(index) {
        const length =  this.projectData.length - 1;
        const full = index === 0 || (index === length && length % 2);
        return {[`xs${full ? '12' : '6'}`]: true};
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
