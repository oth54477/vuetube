<template>
  <div>
    <VideoListItem v-for="(video, index) in videoList" :key="index" :video-info="video" @click-video="clickVideo"/>

  </div>
</template>

<script>
import VideoListItem from '@/components/VideoListItem'

export default {
  name: "VideoList",
  components: {
    VideoListItem,
  },
  props: {
    videoList: Array,
  },
  data: function () {
    return {

    }
  },
  methods: {
    clickVideo: function (videoInfo) {
      this.$emit('click-video', videoInfo)
    }
  },

}
</script>

<style>

</style>