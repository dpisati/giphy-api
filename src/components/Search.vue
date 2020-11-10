<template>
  <div>
    <input
      type="text"
      placeholder="Type something to find a gif..."
      @input="onInput"
      v-model="keyword"
    />
  </div>
</template>

<script>
export default {
  name: "Search",
  data() {
    return {
      keyword: "",
      timeout: null
    };
  },
  methods: {
    onInput() {
      clearTimeout(this.timeout);
      this.timeout = setTimeout(() => {
        this.search();
      }, 500);
    },
    search() {
      if (this.keyword.length == 0) {
        fetch(
          `https://api.giphy.com/v1/gifs/trending?api_key=m6RBYiV6go7FFjHQvmnVxjHYiOZUtOJr&limit=9`
        )
          .then(response => response.json())
          .then(result => {
            this.$emit("fetch-gifs", result.data);
          });
      }
      fetch(
        `https://api.giphy.com/v1/gifs/search?api_key=m6RBYiV6go7FFjHQvmnVxjHYiOZUtOJr&q=${this.keyword}&limit=9`
      )
        .then(response => response.json())
        .then(result => {
          this.$emit("fetch-gifs", result.data);
        });
    }
  }
};
</script>

<style  scoped>
input {
  padding: 10px 16px;
}
</style>

