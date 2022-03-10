<template>
  <main class="main-content">
    <AlbumList />
  </main>
</template>

<script>
import AlbumList from './AlbumList.vue'


export default {
    components: {
    AlbumList
    },
}
</script>

<style lang="scss" scoped>
.main-content {
    background-color: #1E2D3B;
}
</style>