<template>
  <div class="search">
    <img src="../../public/logo.jpg" alt="logo">
    <div class="search-group">
    <input
      type="text"
      placeholder="Type something to find a gif..."
      @input="onInput"
      v-model="keyword"
    />
    <img class="icon" src="../../public/search.png" alt="search" width="28" height="28">
    </div>
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
          `https://api.giphy.com/v1/gifs/trending?api_key=m6RBYiV6go7FFjHQvmnVxjHYiOZUtOJr&limit=8`
        )
          .then(response => response.json())
          .then(result => {
            this.$emit("fetch-gifs", result.data);
          });
      }
      fetch(
        `https://api.giphy.com/v1/gifs/search?api_key=m6RBYiV6go7FFjHQvmnVxjHYiOZUtOJr&q=${this.keyword}&limit=8`
      )
        .then(response => response.json())
        .then(result => {
          this.$emit("fetch-gifs", result.data);
          this.$emit("send-keyword", this.keyword);
        });
    }
  }
};
</script>

<style  scoped>
.search {
  width: 100%;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
  margin: 28px 0;  
  
}

input {
  padding: 10px 16px;
  width: 100%;
  margin: 28px 0;
  height: 40px;
  border-radius: 30px;
  border: none;
  padding-left: 38px;
  padding-right: 38px;
  font-family: 'Ubuntu', sans-serif;
  font-weight: 500;
  font-size: 18px;
}
input::placeholder {
  font-size: 18px;
}
input:focus {
  border: none;
  outline: none;
}

.search-group{
  width: 60%;
  display: flex;
  position: relative;
}

.icon {
  position: absolute;
  right: 28px;
  bottom: 45px;
  background-color: white;
}
</style>

