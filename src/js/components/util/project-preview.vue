<template>
  <div>
    <v-card>
      
      <!-- Card Image -->
      <v-card-media>
        <img :src="imgTest">
      </v-card-media>

      <!-- Text content -->
      <v-card-title>
        Some text
      </v-card-title>

      <!-- Buttons -->
      <v-card-actions>
        <v-btn>Button</v-btn>
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
    }
  }
</script>

<style>

</style>