<template>
  <div id="gallery">
    <Item />
  </div>
</template>

<script>
import Item from './Item.vue'
import apikey from '../api/key.js'

export default {
  name: 'Gallery',
  components: {
      Item
  },
  methods: {
      fetchImages(){
          fetch(`https://api.harvardartmuseums.org/object?apikey=${apikey}`)
          .then(response => response.json())
          .then(result => this.images)
          .catch(error => this.errorMessage )
      }
    },
    data () {
        return {
            images: [],
            errorMessage: ''

        }
    }
}
</script>

<style>
h1 {
  color: yellow;
}
</style>
