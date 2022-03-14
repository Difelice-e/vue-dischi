<template>
  <section>
      <div class="container genre-select">
          <select name="genre" id="select-genre" v-model="genreFilter">
              <option 
              v-for="(genre, i) in genreList" 
              :key="i" 
              :value="genre">{{ genre }}</option>
          </select>
      </div>

      <div class="container album-wrapper">
          <AlbumItem 
          v-for="(album, i) in filteredAlbum"
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
            genreList: [],
            genreFilter: ''
        }
    },
    methods: {
        fetchAlbum: function() {
            axios.get('https://flynn.boolean.careers/exercises/api/array/music')
            .then( res =>{
                this.albumList = res.data.response
                this.getGenre(this.albumList)
            })
            .catch( err =>{
                console.warn(err.response)
            })
        },
        getGenre: function (albumList) { 
            albumList.forEach((el) => {
                const genere = el.genre;
                if (!this.genreList.includes(genere)) {
                    this.genreList.push(genere);
                }
            });
        },
    },
    created() {
        this.fetchAlbum()
    },
    computed: {
        filteredAlbum: function() {
            return this.albumList.filter(el => {
                const {genre} = el

                return genre.toLowerCase().includes(this.genreFilter.toLowerCase())
            })
        }
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
        color: var(--app-text);
    }
}

.album-wrapper {
    display: flex;
    flex-wrap: wrap;
    gap: 25px;
    justify-content: center;
}
</style>