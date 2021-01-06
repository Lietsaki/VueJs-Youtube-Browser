<template>
  <li class="list-group-item media" @click="onVideoSelect">
    <!-- We can also pass props to html elements like the img tag, but we don't have to specify them in the props object, only use v-bind, like 
    we're doing on 'src' to pass in the url of each thumbnail. -->
    <img class="mr-3" :src="thumbnailUrl" />
    <div class="media-body">
      {{ video.snippet.title }}
    </div>
  </li>
</template>

<script>
export default {
  name: 'VideoListItem',
  props: {
    // This video is an object coming from the array of 5 objects that comes from VideoList.vue
    video: Object
  },
  // Computed properties can not only be used to transform data from out data model, but also to shorten or somehow do a calculation in
  // our props as well, since the props are simply data coming from a parent element.
  computed: {
    thumbnailUrl() {
      return this.video.snippet.thumbnails.default.url;
    }
  },
  methods: {
    onVideoSelect() {
      this.$emit('videoSelect', this.video);
    }
  }
};
</script>

<style scoped>
li {
  display: flex;
  cursor: pointer;
}

li:hover {
  background-color: #eee;
}
</style>