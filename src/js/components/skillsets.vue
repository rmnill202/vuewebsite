<template>
  <div>
    <br> <!-- Section title -->
    <h1>Skillsets</h1>
    
    <!-- Each skillset should have it's own card -->
    <v-container fluid grid-list-lg>
      <v-layout row wrap>

        <v-flex v-for="item in skillsets">
          <list-card :value="item" :img-width="'60px'" :gallery-width="'70px'" :width="'250px'"></list-card>
        </v-flex>

      </v-layout>
    </v-container>

    <br><v-divider></v-divider>
  </div>
</template>

<script>
  import ListCard from './util/list-card.vue';  

  export default {
    name: 'skillsets',
    props: ['skillsets'],
    components: {ListCard},
    data() {
      return {
      };
    }
  };
</script>

<style></style>
