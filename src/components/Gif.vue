<template>
  <div>
    <div class="gif" :style="`background-image: url(${gif.images.original.url})`"></div>
    <input ref="url" readonly type="text" :value="gif.images.original.url" />
    <button @click="copyUrl">Copy</button>
  </div>
</template>

<script>
export default {
  name: "GifComponent",
  props: {
    gif: Object
  },
  methods: {
    copyUrl() {
      this.$refs.url.select();
      document.execCommand("copy");
      this.$refs.url.value = "Copied!";
    }
  }
};
</script>

<style  scoped>
.gif {
  width: 240px;
  height: 240px;
  background-repeat: no-repeat;
  background-size: cover;
}
</style>