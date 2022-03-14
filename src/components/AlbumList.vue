<template>
  <section>
      <AlbumSelect 
      @cercaGenere="setGenreToFIlter" 
      @cercaArtista="setArtistToFilter"
      :genreList="genreList" :artistList="artistList"/>

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
import AlbumSelect from './AlbumSelect.vue'

export default {
    components: {
        AlbumItem,
        AlbumSelect
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
        setGenreToFIlter: function (filtroGenere) {
            this.genreFilter = filtroGenere
        },
        setArtistToFilter: function (filtroArtista) {
            this.artistFilter = filtroArtista
        }
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



.album-wrapper {
    display: flex;
    flex-wrap: wrap;
    gap: 25px;
    justify-content: center;
    width: 100%;
}
</style>