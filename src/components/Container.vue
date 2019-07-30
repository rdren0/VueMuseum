<template>
  <div>
    <div id="form">
      <button v-on:click="getImages">Explore</button>
    </div>
    <div id="container">
      <div class="frame" v-for="image in images" v-bind:key="image">
          <img v-bind:src="image.baseimageurl" class="img" />
      </div>
    </div>
  </div>
</template>

<script>
import { key } from "../api/key";

export default {
  name: "Container",
  components: {},
  data() {
    return {
      images: [],
      error: ""
    };
  },
  methods: {
    getImages: function() {
      let page = Math.floor(Math.random() * Math.floor(300));
      fetch(
        `https://api.harvardartmuseums.org/image?page=${page}&apikey=${key}`
      )
        .then(response => response.json())
        .then(result => this.filterImages(result.records))
        .catch(error => this.error);
      page = Math.floor(Math.random() * Math.floor(30));
    },
    inputFetch: function() {},
    filterImages: function(images) {
      console.log(images);
      this.images = images;
    }
  },
  mounted: function() {
    this.getImages(function() {});
  }
};
</script>

<style>
#container {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: space-around;
}
#form {
  display: block;
  margin-bottom: 15px;
}
img {
  height: 245px;
  margin: 5px;
  width: 230px;
}
.frame {
  background-color: #FFF;
  border: solid 5vmin #AF7C49;
  border-bottom-color: #AF7C49;
  border-left-color: #AF7C49;
  border-radius: 2px;
  border-right-color: #A57545;
  border-top-color: #A57545;
  box-shadow: 0 0 5px 0 rgba(0, 0, 0, 0.25) inset,
    0 5px 10px 5px rgba(0, 0, 0, 0.25);
  box-sizing: border-box;
  display: inline-block;
  margin: 15px;
  height: 335px;
  /* padding:8vmin; */
  position: relative;
  text-align: center;
}
.frame:before {
  border-radius: 2px;
  bottom: -2vmin;
  box-shadow: 0 2px 5px 0 rgba(0, 0, 0, 0.25) inset;
  content: "";
  left: -2vmin;
  position: absolute;
  right: -2vmin;
  top: -2vmin;
}
.frame:after {
  border-radius: 2px;
  bottom: -2.5vmin;
  box-shadow: 0 2px 5px 0 rgba(0, 0, 0, 0.25);
  content: "";
  left: -2.5vmin;
  position: absolute;
  right: -2.5vmin;
  top: -2.5vmin;
}
</style>
