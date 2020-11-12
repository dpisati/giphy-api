<template>
  <div class="footer">
    <button @click="random">
      More
      <i class="fas fa-arrow-right"></i>
    </button>
  </div>
</template>

<script>
export default {
  name: "AppFooter",
  data() {
    return {
      randomNumber: 8,
    };
  },
  props: {
    keyword: String
  },
  methods: {
    random() {
      if(this.keyword.length > 0) {
        fetch(
        `https://api.giphy.com/v1/gifs/search?api_key=m6RBYiV6go7FFjHQvmnVxjHYiOZUtOJr&q=${this.keyword}&limit=8&offset=${this.randomNumber}`
        )
        .then(response => response.json())
        .then(result => {
          this.randomNumber = this.randomNumber + 8;
          this.$emit("fetch-gifs", result.data);
        });
      } else {
  fetch(
          `https://api.giphy.com/v1/gifs/trending?api_key=m6RBYiV6go7FFjHQvmnVxjHYiOZUtOJr&limit=8&offset=${this.randomNumber}`
        )
          .then(response => response.json())
          .then(result => {
            this.randomNumber = this.randomNumber + 8;
            this.$emit("fetch-gifs", result.data);
          });
      }
        

    }
  }
};
</script>

<style  scoped>
.footer {
  width: 100%;
  height: 48px;
  display: flex;
  justify-content: center;
  margin: 56px 0;
}

.footer button {
  width: 248px;
  height: 56px;
  border-radius: 28px;
  border: none;
  font-size: 22px;
  font-weight: 400;
  outline: none;
  background: rgb(253,96,96);
  background: linear-gradient(90deg, rgba(253,96,96,1) 0%, rgba(147,39,247,1) 100%);
  color: white;
  transition: all 0.2s;
  -webkit-box-shadow: 0px 0px 16px 2px rgba(0,0,0,0.48); 
box-shadow: 0px 0px 16px 2px rgba(0,0,0,0.48);
}

.footer button:hover {
  cursor: pointer;
  transform: scale(1.1);
}

.fa-arrow-right {
  margin-left: 10px;
}
</style>