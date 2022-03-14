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
    background-color: var(--app-bg);
    height: calc(100vh - 100px);
    display: flex;
    align-items: center;
    justify-content: center;
}
</style>