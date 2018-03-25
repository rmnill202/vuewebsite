<template>
  <div>
    <v-card>
      
      <!-- Card Image -->
      <v-card-media :style="mediaStyle" :src="imgTest">
        <v-card-text>
          <span class="title imageText">{{name}}</span>
        </v-card-text>
      </v-card-media>

      <!-- Buttons -->
      <v-card-actions>
        <!-- Expand button -->
        <v-btn icon @click="expanded = !expanded">
          <v-icon>{{expanded ? 'keyboard_arrow_down' : 'keyboard_arrow_up'}}</v-icon>
        </v-btn>
        
        <v-spacer/>

        <!-- More links -->
        <v-btn flat>Hello</v-btn>
      </v-card-actions>

      <!-- Expandable content -->
      <v-slide-y-transition>
      <v-card-text v-show="expanded" style="text-align: left; padding-top: 0px">
        {{description}}
      </v-card-text>
      </v-slide-y-transition>

    </v-card>
  </div>
</template>

<script>
  export default {
    name: 'project-preview',
    props: ['project', 'mediaHeight'],
    data() {
      return {
        expanded: false,
        name: this.project.name,
        description: this.project.description,
        start: this.project.startDate,
        end: this.project.endDate,
        images: this.project.images,
        imgTest: `${require("../../../assets/gradient.png")}`
      }
    },
    computed: {
      mediaStyle() {
        return {'height': this.mediaHeight || ''};
      }
    },
    watch: {
      project(newProject, oldProject) {
        this.name = newProject.name;
        this.description = newProject.description;
      }
    }
  }
</script>

<style>
  .imageText {
    padding: 5px 25px 5px 25px;
    color: white;
    background-color: rgba(0,0,0,0.3);
  }
</style>