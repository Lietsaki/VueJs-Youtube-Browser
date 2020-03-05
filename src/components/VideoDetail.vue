<template>
  <!-- If video exists (has been passed in to this child component already), render the video -->
  <!-- It's necessary to add this v-if because 'video' is null by default in App.vue -->
  <div class="col-md-8" v-if="video">
    <div class="embed-responsive embed-responsive-16by9">
      <iframe
        id="Iframe"
        class="embed-responsive-item"
        :src="videoUrl"
        frameborder="0"
      ></iframe>
    </div>
    <div class="details">
      <h4>{{ video.snippet.title }}</h4>
      <p>{{ video.snippet.description }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'VideoDetail',
  props: {
    video: Object
  },
  computed: {
    videoUrl() {
      // video.Id is identical to this.video.id.videoId, so we can surround the variable name with curly braces and remove the property name (ES2015 syntax)
      const { videoId } = this.video.id;
      return `https://www.youtube.com/embed/${videoId}`;
    }
  }
};
</script>

<style scoped>
.details {
  margin-top: 10px;
  margin-bottom: 10px;
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 4px;
}
</style>
