<template>
  <div>
    <p>{{ document }}</p>
    <div class="mx-3">
      <iframe frame width="1280" height="720" :src="`https://www.youtube.com/embed/${ this.video.id.videoId }`" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
    </div>
    <div class="mx-3 videoInfo">
      <h2>{{ video.snippet.title }}</h2>
      <hr>
      <p>{{ video.snippet.description }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "MainVideo",
  props: {
    video: Object
  },
  data: function () {
    return {
    }
  },
  methods: {

  },
}
</script>

<style>
/* .videoInfo {
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
} */
</style>