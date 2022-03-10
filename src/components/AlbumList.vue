<template>
  <section>
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
.album-wrapper {
    display: flex;
    flex-wrap: wrap;
    gap: 25px;
    justify-content: center;
}
</style>