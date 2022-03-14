<template>
  <section>
      <div class="container genre-select">
          <select name="genre" id="select-genre">
              <option value="1">1</option>
              <option value="2">2</option>
              <option value="3">3</option>
              <option value="4">4</option>
          </select>
      </div>
      <div class="container album-wrapper">
          <AlbumItem 
          v-for="(album, i) in albumList"
          :key="i" 
          :album="album" />   
      </div>
  </section>
  
</template>

<script>
import axios from 'axios'
import AlbumItem from './AlbumItem.vue'

export default {
    components: {
        AlbumItem
    },
    data() {
        return {
            albumList: [],
        }
    },
    methods: {
        fetchAlbum: function() {
            axios.get('https://flynn.boolean.careers/exercises/api/array/music')
            .then( res =>{
                console.log(res.data.response)
                this.albumList = res.data.response
                console.log(this.albumList)
            })
            .catch( err =>{
                console.warn(err.response)
            })
        }
    },
    created() {
        this.fetchAlbum()
    }
}
</script>

<style lang="scss" scoped>
.genre-select {
    text-align: center;
    margin-bottom: 30px;

    select {
        width: 150px;
        background-color: transparent;
        color: white;
    }
}

.album-wrapper {
    display: flex;
    flex-wrap: wrap;
    gap: 25px;
    justify-content: center;
}
</style>