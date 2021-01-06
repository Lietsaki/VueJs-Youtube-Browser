<template>
  <div class="container">
    <SearchBar @TermChange="onTermChange"></SearchBar>
    <div class="row">
      <videoDetail :video="selectedVideo"></videoDetail>
      <!-- NOTE1 :videos is the same as saying v-bind:videos="videos" -->
      <!-- NOTE2 :videos is the name that we asign to the data(the prop) we're sending to our child, this is how we'll refer to it on VideoList.vue 
      Inside the double quotes we put the name of the data property that we're sending as it appers in this file, in this case, "videos".
      LEFT SIDE = property name in child component || RIGHT SIDE = property name in parent component -->
      <VideoList
        @videoSelect="onVideoSelect"
        :videos="videos"
        :pickedAVideo="pickedAVideo"
      ></VideoList>
    </div>
  </div>
</template>

<script>
// Note: In order to use data in a vue component (this file is a vue component), we must use functions that return an object.
// In a vue instance (which is what we have in main.js) we can use the data object (Like this 'data: {}').
// This is because every app instance of our component would have the same reference to the data object if we used it in a component.
// In order to give every component their own copy of the data object, we must create a function that returns an object.
import axios from 'axios';
import SearchBar from './components/SearchBar';
import VideoList from './components/VideoList';
import VideoDetail from './components/VideoDetail';

export default {
  name: 'App',
  components: {
    SearchBar,
    VideoList,
    VideoDetail,
  },
  data() {
    return { videos: [], selectedVideo: null, pickedAVideo: false };
  },
  methods: {
    // We receive searchTerm from the termChange event in searchBar.vue
    onTermChange(searchTerm) {
      axios
        .get('https://www.googleapis.com/youtube/v3/search', {
          params: {
            key: process.env.VUE_APP_APIKEY,
            type: 'video',
            part: 'snippet',
            q: searchTerm,
          },
        })
        .then((response) => {
          this.videos = response.data.items;
          console.log(response);
        })
        .catch((err) => console.log(err));
    },
    onVideoSelect(video) {
      this.selectedVideo = video;
      this.pickedAVideo = true;
    },
  },
  mounted() {
    console.log();
  },
};
</script>

<style></style>
