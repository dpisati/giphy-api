<template>
  <div>
    <div @click="Clipboard_CopyTo(gif.images.original.url)" class="gif" :style="`background-image: url(${gif.images.original.url})`">
      <div id="lottie" :class="{ copied: copied }">
        <lottie-animation
          v-if="copied"
          :loop="false"
          :width="140"
          :height="140"
          path="success.json"
        />
        <h3 v-if="copied" :class="{ copiedText: copied}">Copied</h3>
      </div>  
    </div>
  </div>
</template>

<script>
import LottieAnimation from "lottie-vuejs/src/LottieAnimation.vue"; // import lottie-vuejs
export default {
  name: "GifComponent",
  data() {
    return {
      copied: false,
    };
  },
  components: {
    LottieAnimation
  },
  props: {
    gif: Object
  },
  methods: {
    Clipboard_CopyTo(value) {
      this.copied = true;
      var tempInput = document.createElement("input");
      tempInput.value = value;
      document.body.appendChild(tempInput);
      tempInput.select();
      document.execCommand("copy");
      document.body.removeChild(tempInput);
      setTimeout(() => { this.copied = false; }, 3000);
    }
  }
};
</script>

<style  scoped>
@import url('https://fonts.googleapis.com/css2?family=Goldman&display=swap');
.gif {
  position: relative;
  width: 240px;
  height: 240px;
  background-repeat: no-repeat;
  background-size: cover;
  margin: 12px;
  border-radius: 18px;
  transition: 0.2s;
}
.gif:hover {
  cursor: pointer;
  transform: scale(1.1);
}
#lottie{
  height: 240px;
  width: 240px;
  position: absolute;
  top: 0;
  left: 0;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  border-radius: 18px;
}


.copied {
  transition: 1s;
  background-color: rgba(48, 48, 48, 0.9);
}
h3 {
  font-family: 'Goldman', cursive;
  color: #6BC859;
  font-size: 38px;
  margin: 0;
  transition: color 10s;  
}

</style>