<template>
  <div>
    <h1>{{anime.title}}</h1>
    <img :src="anime.image_url" />
    <h1>{{anime.score}}</h1>
  </div>
</template>

<script>
export default {
  props: {
    anime: {
      type: Object,
      default: () => ({})
    }
  }
};
</script>

<style>
</style>