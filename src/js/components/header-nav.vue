<template>
  <div>
    <v-toolbar flat dense>
      <!-- Icons on the left side of the toolbar -->
      <v-btn icon v-for="link in leftLinks" :key="link.id" :href="link.address" target="_blank" rel="noopener noreferrer" class="hidden-xs-only">
        <v-icon>{{link.icon.icon}}</v-icon>
      </v-btn>

      <v-spacer></v-spacer>

      <!-- For larger screens, display all buttons -->
      <v-toolbar-items class="hidden-sm-and-down">
        <v-btn v-for="link in rightLinks" :href="link.address" :key="link.id" flat>{{link.text}}</v-btn>
      </v-toolbar-items>

      <!-- For smaller screens, display a menu -->
      <v-menu transition="slide-x-transition" class="hidden-md-and-up" left>
        <!-- Hamburger menu icon! -->
        <v-btn icon slot="activator"> <v-icon>menu</v-icon> </v-btn>
        <!-- The menu contents -->
        <v-list>
          <!-- Buttons from the right side of the toolbar -->
          <v-list-tile @click="" v-for="link in rightLinks" :key="link.id" :href="link.address">
            <v-list-tile-title> {{link.text}} </v-list-tile-title>
          </v-list-tile>
          <!-- Links from the left side of the toolbar -->
          <v-divider class="hidden-sm-and-up"></v-divider>
          <v-list-tile @click="" v-for="link in leftLinks" :key="link.id" :href="link.address" target="_blank" class="hidden-sm-and-up">
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
