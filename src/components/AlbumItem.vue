<template>
  <div class="album-card card">
    <figure>
        <img :src="album.poster" alt="">
    </figure>
    {{ album.title }}
  </div>
</template>

<script>
export default {
    props: {
        album: {
            type: Object,
            required: true,
        }
    }
}
</script>

<style lang="scss" scoped>

</style>