<template>
  <div id="gif-list">
    <gif v-for="gif in gifs" :key="gif.id" :gif="gif" />
  </div>
</template>

<script>
import Gif from "./Gif";
export default {
  name: "GifList",
  components: {
    Gif
  },
  props: {
    gifs: Array
  }
};
</script>

<style  scoped>
#gif-list {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
  align-items: center;
  margin-top: 24px;
}
</style>