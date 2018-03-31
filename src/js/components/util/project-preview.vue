<template>
  <div>
    <v-card :style="cardStyle">
      
      <!-- Card Image -->
      <v-card-media :style="mediaStyle" :src="image">
        <v-card-text>
          <span class="title imageText">{{name}}</span>
          <div v-if="tags" class="tagContainer">
            <!-- <v-icon v-for="tag in tags">{{tag.icon}}</v-icon> -->
            <!-- <v-btn icon v-for="tag in tags" style="margin: 5px 0 0 0">
              <v-icon color="white">{{tag.icon}}</v-icon>
            </v-btn> -->
            <template v-for="tag in tags">
              <v-tooltip bottom>
                <v-icon color="white" slot="activator" style="padding-right: 10px">{{tag.icon}}</v-icon>
                <span>{{tag.text}}</span>
              </v-tooltip>
            </template>
          </div>
        </v-card-text>
      </v-card-media>

      <!-- Buttons -->
      <v-card-actions>
        <!-- Tagline -->
        <span class="">{{description}}</span>
      </v-card-actions>

      <v-card-actions>
        <template v-if="start && end">
          <span class="dateDisplay">{{`${start} - ${end}`}}</span>
          <!-- <v-btn color="grey darken-1 white--text" small>{{`${start} - ${end}`}}</v-btn> -->
        </template>

        <v-spacer/>

        <v-btn raised v-for="link in links" :key="link.text" color="grey darken-1 white--text" small target="_blank" rel="noopener noreferrer" :href="link.url">{{link.text}}</v-btn>
      </v-card-actions>
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
        links: this.project.links,
        tags: this.project.tags
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
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    padding: 5px 0 5px 0;
    color: white;
    background-color: rgba(0,0,0,0.3);
  }
  .tagContainer {
    position: absolute;
    bottom: 0;
    left: 0;
    padding: 0 5px 5px 5px;
    width: 100%;
    text-align: left;
    background-color: rgba(0,0,0,0.3);
  }
  .dateDisplay {
    padding: 2px 8px 2px 8px;
    /* background-color: lightgray; */
    background-color: #757575;
    color: white;
    border-radius: 2px;
  }
  .linkButtons {
    color: white;
  }
</style>