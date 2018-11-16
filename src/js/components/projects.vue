<template>
  <div>
    <br> <!-- Section title -->
    <h1 id="projects">Projects</h1>
    
    <!-- Container for the two columns displayed on larger screens -->
    <div class="hidden-sm-and-down larger"> 

      <!-- Display the projects in a flexbox -->
      <div>
        <diamond-grid :elements="images" :pattern="[1,2]" 
            :selection="selectedIndex" @selected="updateSelected" 
            :width="120" :height="120" 
            class="hidden-sm-and-down"></diamond-grid>
      </div>
      
      <!-- Whatever project is selected, display a preview! -->
      <v-slide-x-reverse-transition mode="out-in">
        <project-preview v-if="selected" :key="selected.key" :project="selected" :mediaHeight="'450px'" :width="'450px'"/>
      </v-slide-x-reverse-transition>
    </div>

    <!-- Container for accordion displayed on smaller screens -->
    <div class="hidden-md-and-up smaller">
      <v-container fluid grid-list-lg>
        <v-layout row wrap>
          
          <!-- Project preview -->
          <v-flex v-for="(project, index) in projectData" xs12> 
            <project-preview :project="projectData[projectData.length -1 -index]" :mediaHeight="'120px'"/>
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
        selectedIndex: 4 
      };
    },
    computed: {
      /** 
       * Images to be used for the grid of diamonds.
       */
      images() {
        const projectData = [];

        //Loop through each project and gather the following data:
        for(let i = 0; i < this.projects.length; i++) {
          projectData.push(this.getImage(this.projects[i].preview.images));
        }

        return projectData;
      },
      /** 
       * Pull out any necessary project data into an array of objects.
       */
      projectData() {
        const projectData = [];

        //Loop through each project and gather the following data:
        for(let i = 0; i < this.projects.length; i++) {
          const proj = this.projects[i];
          projectData.push({
            'name': proj.preview.name, //Name
            'description': proj.preview.description, //Description
            'image': this.getImage(proj.preview.images), //First image OR default image
            'startDate': proj.preview.startDate,
            'endDate': proj.preview.endDate,
            'links': proj.preview.links,
            'tags': proj.preview.tags,
            'key': i
          });
        }

        return projectData;
      },
      /** 
       * The currently selected object.
       */
      selected() {
        return this.projectData[this.selectedIndex];
      }
    },
    methods: {
      /** 
       * Update the currently selected project.
       */
      updateSelected(newIndex) {
        this.selectedIndex = (newIndex === this.selectedIndex) ? -1 : newIndex;
      },
      /** 
       * Given an array of project images, load the first image, or a placeholder if the
       *   array is empty.
       */
      getImage(images) {
        if(!images || !images.length) {
          return require(`../../assets/gradient.png`);
        } else {
          return require(`../../assets/${images[0].img}`);
        }
      },
      /** 
       * Meant for determining the number of grid-spaces to be taken up by a project in
       *   the smaller project view. Not used right now, but might be used again.
       */
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
    display: flex;
    justify-content: space-around;
    grid-template-columns: 40% 10% 40%;
  }
  .smaller {
    margin-left: 5%;
    margin-right: 5%;
  }
</style>
