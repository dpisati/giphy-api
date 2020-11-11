<template>
  <div>
    <search @fetch-gifs="onFetch" />
    <gif-list :gifs="gifs" />
  </div>
</template>

<script>
import Search from "./components/Search";
import GifList from "./components/GifList";

export default {
  name: "App",
  components: {
    Search,
    GifList
  },
  data() {
    return {
      gifs: []
    };
  },
  mounted() {
    fetch(
      `https://api.giphy.com/v1/gifs/trending?api_key=m6RBYiV6go7FFjHQvmnVxjHYiOZUtOJr&limit=9`
    )
      .then(response => response.json())
      .then(result => {
        this.gifs = result.data;
      });
  },
  methods: {
    onFetch(result) {
      this.gifs = result;
    }
  }
};
</script>
