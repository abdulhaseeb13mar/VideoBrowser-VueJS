<template>
  <ul class="list-group">
    <VideoListItem
      v-for="video in videos"
      :key="video.etag"
      :video="video"
      @videoSelect="onVideoSelect"
    ></VideoListItem>
  </ul>
</template>

<script>
import VideoListItem from "./VideoListItem";
export default {
  name: "VideoList",
  components: {
    VideoListItem,
  },
  props: ["videos"],
  methods: {
    onVideoSelect: function(video) {
      this.$emit("videoSelect", video);
    },
  },
};
</script>

<style scoped></style>
