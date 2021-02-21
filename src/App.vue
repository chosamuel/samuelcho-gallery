<template>
  <div id="app">
    <transition name="fade">
      <div
        v-if="lightboxOn"
        class="lightbox"
        v-on:click="lightboxOn = !lightboxOn"
      >
        <div class="video-container">
          <video autoplay loop>
            <source
              :src="getVid(currentID)"
              class="vid"
            />
          </video>
        </div>
      </div>
    </transition>
    <div>
      <div class="title">
      <h1>_samuelcho_</h1>
      <div class="text">
        <div>a collection of my sketches</div>
        <div>click on thumbnail to see video</div>
        <div>
          &nbsp;<a href="https://www.instagram.com/_samuelcho_/">instagram</a>&nbsp;
          &nbsp;<a href="https://twitter.com/_samuelcho">twitter</a>&nbsp;
          &nbsp;<a href="https://samuelcho.de">website</a>&nbsp;
          </div>
      </div>
      </div>
    </div>
    <div class="gallery">
      <div class="left column">
        <div v-for="(sketch, index) in index" :key="index">
          <img
            v-on:click="view(sketch)"
            v-if="index % 2 == 0"
            :src="getImg(sketch)"
            alt=""
            class="sketch"
          />
        </div>
      </div>
      <div class="right column">
        <div v-for="(sketch, index) in index" :key="index">
          <img
            v-on:click="view(sketch)"
            v-if="index % 2 == 1"
            :src="getImg(sketch)"
            alt=""
            class="sketch"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data: () => ({
    index: [
      "0001", "0002", "0003", "0004", "0005",
      "0006", "0007", "0008", "0009", "0010",
      "0011", "0012", "0013", "0014", "0015",
      "0016", "0017", "0018", "0019", "0020",
      "0021", "0022", "0023", "0024", "0025",
      "0026", "0027", "0028", "0029", "0030",
      "0031", "0032", "0033", "0034", "0035",
      "0036", 
    ],
    lightboxOn: false,
    currentID: null,
  }),
  mounted: function () {
    this.index = this.index.reverse();
  },
  methods: {
    getImg: function (image) {
      return require(`./assets/images/${image}.png`);
    },
    getVid: function (video) {
      return require(`./assets/videos/${video}.mp4`);
    },
    view: function (id) {
      this.lightboxOn = true;
      this.currentID = id;
      console.log(id);
    },
  },
};
</script>

<style>
@font-face {
  font-family: "Plain";
  src: url("./assets/fonts/Plain-Light.ttf") format("truetype");
}
* {
  padding: 0;
  margin: 0;
  font-family: "Plain";
}
.gallery {
  display: flex;
  justify-content: center;
  position: relative;
  max-width: 1024px;
  margin: auto;
}
.sketch {
  width: 100%;
  /* margin: 0.25vh; */
}

.column {
  width: 50%;
  margin: 0.5vh 0.5vh;
}

.lightbox {
  width: 100vw;
  height: 100vh;
  position: fixed;
  background-color: rgba(0, 0, 0, 0.9);
  z-index: 999;
}

.fade-enter,
.fade-leave-to {
  opacity: 0;
}

.fade-enter-active,
.fade-leave-active {
  transition: 0.5s;
}

.video-container {
  width: 55vw;
  min-width: 80vw;
  max-width: 720px;
  height: 60vh;
  margin: auto;
  margin-top: 10vh;
  opacity: 100%;
}
video {
  display: block;
  width: 100%;
  margin: auto;
}

.title {
  text-align: center;
}

h1 {
  font-size: 2em;
  padding-top: 2vh;
}

.text {
  margin-bottom: 5vh;
  font-size: 0.75em;
  color: gray;
}
</style>
