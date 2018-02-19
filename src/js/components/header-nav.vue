<template>
  <div>
    <v-toolbar flat dense>
      <v-btn icon v-for="link in leftLinks">
        <v-icon>{{link.icon.icon}}</v-icon>
      </v-btn>

      <v-spacer></v-spacer>

      <!-- For larger screens -->
      <v-toolbar-items class="hidden-sm-and-down">
        <v-btn v-for="link in rightLinks" flat>{{link.text}}</v-btn>
      </v-toolbar-items>

      <!-- For smaller screens -->
      <v-menu transition="slide-x-transition" class="hidden-md-and-up">

        <!-- Hamburger menu icon! -->
        <v-btn icon slot="activator"> <v-icon>menu</v-icon> </v-btn>

        <!-- The menu contents -->
        <v-list>
          <v-list-tile @click="" v-for="link in rightLinks">
            <v-list-tile-title> {{link.text}} </v-list-tile-title>
          </v-list-tile>
        </v-list>
      </v-menu>

    </v-toolbar>
  </div>
</template>

<script>
  export default {
    name: 'header-nav',
    props: ['headerLinks'],
    data() {
      return {
        leftLinks: this.headerLinks.left,
        rightLinks: this.headerLinks.right
      };
    },
  };
</script>

<style></style>
