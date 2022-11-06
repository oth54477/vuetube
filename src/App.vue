<template>
  <body>
    <div id="container">
        <div class="m-2" id="banner">
          <img src="@/assets/logo.png" alt="Logo" style="height: 45%; display:inline;">
          <h1 style="display:inline">VueTube</h1>
        </div>
        <div class="my-4 mx-5" id="search">
          <SearchBar @data-to-app="search"/>
        </div>
      <article class="" id="videoPlay">
        <MainVideo :video="mainVideo"/>
      </article>
      <article id="videoList">
        <VideoList :video-list="videoList" @click-video="clickVideo"/>
      </article>
    </div>
  </body>
</template>

<script>
import axios from 'axios'

import MainVideo from '@/components/MainVideo'
import SearchBar from '@/components/SearchBar'
import VideoList from '@/components/VideoList'

const API_KEY = process.env.VUE_APP_YOUTUBE_API_KEY
const API_URL = "https://www.googleapis.com/youtube/v3/search"

export default {
  name: 'App',
  components: {
    MainVideo,
    SearchBar,
    VideoList,
  },
  data: function () {
    return {
      videos: null,
      inputData: null,
      mainVideo: null,
      videoList: null,
    }
  },
  methods: {
    search: function (inputData) {
      console.log(inputData)
      console.log(API_KEY)
      this.inputData = inputData
      axios({
        method: "get",
        url: API_URL,
        params: {
          key: API_KEY,
          part: "snippet",
          type: "video",
          q: this.inputData
        }
      })
        .then((response) => {
          this.videos = response.data.items
          this.mainVideo = this.videos[0]
          this.videoList = this.videos.slice(1, this.videos.length)
        })
        .catch((error) => {
          console.log(error)
        })
    },
    clickVideo: function (videoInfo) {
      this.mainVideo = videoInfo
      this.videoList = this.videos.filter(video => video.etag !== videoInfo.etag)
    }
  },
}
</script>

<style>
/* #container {
  width: 100vw;
  height: 100vh;
  display: grid;
  grid-template-columns: repeat(10, 10%);
  grid-auto-rows: 10% 90%;
}
@media (min-width: 1900px) {
  #videoPlay {
    grid-column: 1/11;
    grid-row: 2/7;
  }
  #videoList {
    grid-column: 1/11;
    grid-row: 7/11;
  }
}
#banner {
  grid-column: 1/3;
  grid-row: 1/2;
}
#search {
  grid-column: 10/11;
  grid-row: 1/2;
}
#videoPlay {
  grid-column: 1/7;
  grid-row: 2/11;
}
#videoList {
  grid-column: 8/11;
  grid-row: 2/11;
} */


@media (min-width: 1800px) {
  #container {
    display: grid;
    grid-template: "banner search"
    "videoPlay videoPlay videoList videoList"
    "videoPlay videoPlay videoList videoList";
  }
}

@media (min-width: 0px) {
  #container {
    display: grid;
    grid-template: "banner search"
    "videoPlay videoPlay"
    "videoList videoList";
  }  
}

#banner {
  grid-area: banner;
}
#search {
  text-align: right;
  grid-area: search;
}
#videoPlay {
  grid-area: videoPlay;
}
#videoList {
  grid-area: videoList;
}

</style>
