<template>
  <div class="main">
    <search @fetch-gifs="onFetch" @send-keyword="searchWord" />
    <gif-list :gifs="gifs" />
    <app-footer @fetch-gifs="onFetch" :keyword="keyword"/>
  </div>
</template>

<script>
import Search from "./components/Search";
import GifList from "./components/GifList";
import AppFooter from "./components/AppFooter";

export default {
  name: "App",
  components: {
    Search,
    GifList,
    AppFooter
  },
  data() {
    return {
      gifs: [],
      keyword: ''
    };
  },
  mounted() {
    fetch(
      `https://api.giphy.com/v1/gifs/trending?api_key=m6RBYiV6go7FFjHQvmnVxjHYiOZUtOJr&limit=8`
    )
      .then(response => response.json())
      .then(result => {
        this.gifs = result.data;
      });
  },
  methods: {
    onFetch(result) {
      this.gifs = result;
      window.scrollTo(0,0);
    },
    searchWord(word) {
      this.keyword = word;
    }
  }
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Ubuntu:wght@400;500&display=swap');
* {
  padding: 0;
  margin: 0;
  font-family: 'Ubuntu', sans-serif;
  font-weight: 500;
  scroll-behavior: smooth;

}
body {
    background-image:
    radial-gradient(
       #121214,
      #131314
    );
}
.main {
  max-width: 1080px;
  margin-left: auto;
  margin-right: auto;
}

</style>

