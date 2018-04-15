<template>
  <div>
    <br> <!-- Section title -->
    <h1>About Me</h1>
    
    <!-- Each "About Me" section should be a card in the flex container -->
    <v-container fluid grid-list-lg>
      <v-layout row wrap>

        <v-flex v-for="item in about">
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
    name: 'about',
    props: ['about'],
    components: {ListCard},
    data() {
      return {
      };
    }
  };
</script>

<style></style>
