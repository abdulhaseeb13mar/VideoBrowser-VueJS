<template>
  <div class="container">
    <SearchBar @termChange="onTermChange"></SearchBar>
    <div class="row">
    <VideoDetail :video="selectedVideo"></VideoDetail>
    <VideoList :videos="videos" @videoSelect="onVideoSelect"></VideoList>

    </div>
  </div>
</template>

<script>
import axios from "axios";
import SearchBar from "./components/SearchBar";
import VideoList from "./components/VideoList";
import VideoDetail from "./components/VideoDetail";
// const API_KEY = "AIzaSyABW_SeHyvy_kDYIIszqpG2KqTiP4PmxOs"; //abdulhaseeb13mar@gmail.com
const API_KEY = "AIzaSyA6pO_V0_pVpEHe-HrFLZkbDs80RUBRFXI"; //abdulhaxeeb50@gmail.com


export default {
  name: "App",
  components: {
    SearchBar,
    VideoList,
    VideoDetail,
  },
  data: function() {
    return { videos: [], selectedVideo: null };
  },
  methods: {
    onTermChange: function(searchTerm) {
      console.log("search term", searchTerm);
      axios
        .get("https://www.googleapis.com/youtube/v3/search", {
          params: {
            key: API_KEY,
            type: "video",
            part: "snippet",
            q: searchTerm,
          },
        })
        .then((res) => {
          this.videos = res.data.items;
        })
        .catch((err) => console.log(err));
    },
    onVideoSelect: function(video) {
      this.selectedVideo = video;
      console.log(video);
    },
  },
};
</script>
