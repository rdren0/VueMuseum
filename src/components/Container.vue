<template>
  <div>
    <div class="form">
      <button id="explore" v-on:click="getImages">Explore</button>
    </div>
    <div id="container">
      <div v-for="(image, index) in images" v-bind:key="index" class="frame">
        <img v-bind:src="image.baseimageurl" class="img" />
      </div>
    </div>
    <div class="footer-btn">
      <button class="page" v-on:click="previous">⬅ Previous</button>
      <button class="page" v-on:click="next">Next ➡</button>
    </div>
  </div>
</template>

<script>

export default {
  name: "Container",
  components: {},
  data() {
    return {
      images: [],
      page: 1,
      error: ""
    };
  },
  methods: {
    fetch: function() {
      fetch(
        `https://api.harvardartmuseums.org/image?size=10&page=${this.page}&apikey=${process.env.VUE_APP_KEY}`
      )
        .then(response => response.json())
        .then(result => this.filterImages(result.records))
        .catch(error => this.error);
    },
    getImages: function() {
      let page = Math.floor(Math.random() * Math.floor(1000));
      this.page = page;
      this.fetch();
    },
    previous: function() {
      this.page = this.page - 1;
      this.fetch();
    },
    next: function() {
      this.page = this.page + 1;
      this.fetch();
    },
    filterImages: function(images) {
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
  display: flex;
  justify-content: space-around;
}
button {
  min-width: 250px;
  height: 60px;
  padding: 0;
  margin-top: -30px;
  font-size: 30px;
  color: #DDBC00;
  vertical-align: middle;
  background: black;
  border: #8f6b29 2px solid;
}
button:hover {
  cursor: pointer;
}
.page {
  margin-top: 10px;
  margin: 10px;
  width: 180px;
}
.footer-btn {
  display: block;
}
img {
  height: 255px;
  padding: 5px;
}

.frame {
  background-color: #fff;
  border: solid 5vmin #af7c49;
  border-bottom-color: #af7c49;
  border-left-color: #af7c49;
  border-radius: 2px;
  border-right-color: #a57545;
  border-top-color: #a57545;
  box-shadow: 0 0 5px 0 rgba(0, 0, 0, 0.25) inset,
    0 5px 10px 5px rgba(0, 0, 0, 0.25);
  box-sizing: border-box;
  display: inline-block;
  margin: 15px;
  height: 335px;
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
