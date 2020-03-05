<template>
  <ul :class="pickedAVideo ? colSpan4 : colSpan12">
    <!-- Bind each one of the 5 videos returned by the YT API to our child component VideoListItem.vue and pass them as props called 
      video -->
    <VideoListItem
      v-for="videoResult in videos"
      :key="videoResult.etag"
      :video="videoResult"
      @videoSelect="onVideoSelect"
    ></VideoListItem>
  </ul>
</template>

<script>
import VideoListItem from './VideoListItem';

export default {
  name: 'VideoList',
  data() {
    return {
      colSpan4: 'list-group col-md-4',
      colSpan12: 'list-group col-md-12'
    };
  },
  components: {
    VideoListItem
  },
  // Props is data that we expect to get from a parent element. For instance, 'videos' is an array containing 5 objects
  // that we get from App.vue, and each one of those objects contains data about one video.
  props: {
    videos: Array,
    pickedAVideo: Boolean
  },
  methods: {
    // Note: 'video' is the data that we received from the videoSelect event from VideoListItem.vue
    onVideoSelect(video) {
      this.$emit('videoSelect', video);
    }
  }
};
</script>


<style>
</style>