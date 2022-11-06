<template>
  <div class="videoList" @click="clickVideo">
    <img :src="videoInfo.snippet.thumbnails.default.url" :width="videoInfo.snippet.thumbnails.default.width" :height="videoInfo.snippet.thumbnails.default.height" alt="No img">
    <p>{{ videoInfo.snippet.title }}</p>
    <hr>
  </div>
</template>

<script>
export default {
  name: "VideoListItem", 
  props: {
    videoInfo: Object
  },
  data: function () {
    return {
    }
  },
  methods: {
    clickVideo: function () {
      this.$emit('click-video', this.videoInfo)
    }
  },
}
</script>

<style>
.videoList {
  display: flex;
  align-items: center;

}

</style>