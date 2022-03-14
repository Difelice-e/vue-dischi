<template>
  <section>
      <div class="container filter-select">
          <label for="select-genre">Generi Musicali:</label>
          <select name="genre" id="select-genre" v-model="genreFilter">
              <option value="">Tutti</option>
              <option 
              v-for="(genre, i) in genreList" 
              :key="i" 
              :value="genre">{{ genre }}</option>
          </select>
          
          <label for="select-artist">Artista:</label>
          <select name="artist" id="select-artist" v-model="artistFilter">
              <option value="">Tutti</option>
              <option 
              v-for="(artist, i) in artistList" 
              :key="i" 
              :value="artist">{{ artist }}</option>
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
            genreFilter: '',
            artistList: [],
            artistFilter: ''
        }
    },
    methods: {
        fetchAlbum: function() {
            axios.get('https://flynn.boolean.careers/exercises/api/array/music')
            .then( res =>{
                this.albumList = res.data.response
                this.getGenre(this.albumList)
                this.getArtist(this.albumList)
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
        getArtist: function (albumList) { 
            albumList.forEach((el) => {
                const artista = el.author;
                if (!this.artistList.includes(artista)) {
                    this.artistList.push(artista);
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
                const {genre, author} = el

                return genre.toLowerCase().includes(this.genreFilter.toLowerCase()) &&
                author.toLowerCase().includes(this.artistFilter.toLowerCase())
            })
        },
    }
}

</script>

<style lang="scss" scoped>
section {
    width: 100%;
}

.filter-select {
    text-align: center;
    margin-bottom: 30px;

    label {
        color: white;
        margin-right: 5px;
    }

    select {
        width: 150px;
        background-color: transparent;
        color: var(--app-text);
        margin-right: 20px;
    }
}

.album-wrapper {
    display: flex;
    flex-wrap: wrap;
    gap: 25px;
    justify-content: center;
    width: 100%;
}
</style>