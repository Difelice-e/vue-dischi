<template>
  <div class="album-card card">
    <figure class="album__cover">
      <img :src="album.poster" alt="" />
    </figure>

    <div class="album__info">
      <h4 class="album__title">{{ album.title }}</h4>
      <p class="album__author">{{ album.author }}</p>
      <p class="album__year">{{ album.year }}</p>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    album: {
      type: Object,
      required: true,
    },
  },
};
</script>

<style lang="scss" scoped>
.album-card {
  background-color: #2E3A46;
  width: 18%;
  padding: 20px 20px 10px;
}

.album__cover {
  width: 100%;
  aspect-ratio: 1/1;
  margin-bottom: 20px;

  img {
      object-fit: cover;
      object-position: center;
  }
}

.album__info {
  text-align: center;

  .album__title {
    text-transform: uppercase;
    color: white;
    font-size: 1.5rem;
    margin-bottom: 20px;
  }

  .album__author {
      color: #727F7C;
  }

  .album__year {
      color: #727F7C;
  }
}
</style>