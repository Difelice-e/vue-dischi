<template>
  <div class="album-card card">
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