<template>
  <div>
    <v-card>
      
      <!-- Card Image -->
      <v-card-media>
        <img :src="imgTest">
      </v-card-media>

      <!-- Text content -->
      <v-card-title>
        <div style="text-align: left">
          <h3 class="headline mb-0">{{name}}</h3>
          <div>{{description}}</div>
        </div>

      </v-card-title>

      <!-- Buttons -->
      <v-card-actions>
        <v-btn flat>More</v-btn>
      </v-card-actions>

    </v-card>
  </div>
</template>

<script>
  export default {
    name: 'project-preview',
    props: ['project'],
    data() {
      return {
        name: this.project.name,
        description: this.project.description,
        start: this.project.startDate,
        end: this.project.endDate,
        images: this.project.images,
        imgTest: `${require("../../../assets/gradient.png")}`
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

</style>