<template>
  <div id="app">

    <MainHeader />
    <MainContent/>

  </div>
</template>

<script>
import MainHeader from './components/MainHeader.vue'
import MainContent from './components/MainContent.vue'

export default {
  name: 'App',
  components: {
    MainHeader,
    MainContent
  }
}
</script>

<style lang="scss">
@import './assets/scss/common.scss';  // importo extra css 
@import './assets/scss/mixins.scss';

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
