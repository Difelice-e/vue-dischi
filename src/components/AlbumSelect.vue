<template>
  <section>
      <div class="container filter-select">
          <label for="select-genre">Generi Musicali:</label>
          <select @change="filtraAlbumGenere" name="genre" id="select-genre" v-model="genreFilter">
              <option value="">Tutti</option>
              <option 
              v-for="(genre, i) in genreList" 
              :key="i" 
              :value="genre">{{ genre }}</option>
          </select>
          
          <label for="select-artist">Artista:</label>
          <select @change="filtraAlbumArtista" name="artist" id="select-artist" v-model="artistFilter">
              <option value="">Tutti</option>
              <option 
              v-for="(artist, i) in artistList" 
              :key="i" 
              :value="artist">{{ artist }}</option>
          </select>
      </div>
  </section>
</template>

<script>
export default {
    props: {
        genreList: Array,
        artistList: Array,
    },
    data() {
        return {
        genreFilter: '',
        artistFilter: ''
        }
    },
    methods: {
    filtraAlbumGenere: function() {
        this.$emit('cercaGenere', this.genreFilter)
        },
    
    filtraAlbumArtista: function() {
        this.$emit('cercaArtista', this.artistFilter)
        console.log(this.artistFilter)
        }
    },
}
</script>

<style lang="scss" scoped>
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
</style>