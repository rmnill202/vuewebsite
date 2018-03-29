<template>
  <div>
    <v-card :style="cardStyle">
      
      <!-- Card Image -->
      <v-card-media :style="mediaStyle" :src="image">
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
        <v-btn flat v-for="link in links" :key="link.text" target="_blank" rel="noopener noreferrer" :href="link.url">{{link.text}}</v-btn>
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
    props: ['project', 'mediaHeight', 'width'],
    data() {
      return {
        expanded: true,
        name: this.project.name,
        description: this.project.description,
        start: this.project.startDate,
        end: this.project.endDate,
        image: this.project.image,
        links: this.project.links
      }
    },
    computed: {
      /** 
       * Styling to be used for the preview image/text section.
       */
      mediaStyle() {
        return {'height': this.mediaHeight || ''};
      },
      cardStyle() {
        return {'width': this.width || ''};
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