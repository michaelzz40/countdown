<template>
  <div id="app">
    <Navbar />
    <div class="circle" v-if="appear">
      <img src="./assets/firework.jpg" alt />
    </div>
    <span class="drop"></span>
    <Home></Home>
  </div>
</template>

<script>
import Home from "./views/Home";
import Navbar from "./components/Navbar";
export default {
  data() {
    return {
      appear: false
    };
  },
  name: "App",
  components: {
    Home: Home,
    Navbar
  },
  methods: {
    loadImage() {
      setTimeout(() => {
        this.appear = true;
      }, 2000);
    }
  },
  mounted() {
    this.loadImage();
  }
};
</script>

<style>
* {
  font-family: "Roboto", sans-serif;
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

body {
  background: rgba(255, 255, 255, 1);
  color: #f4f4f4;
  overflow-x: hidden;
  z-index: 1;
}

.circle {
  position: absolute;
  top: 0;
  background-color: rgba(235, 195, 219, 0.9);
  z-index: -1;
  animation: pop 1s forwards;
  overflow: hidden;
  transform: translate(-50%, -50%);
}

.circle img {
  max-width: 100%;
}

@keyframes pop {
  0% {
    opacity: 0.5;
    border-radius: 100%;
    transform: scale(0.1);
  }
  100% {
    opacity: 1;
    border-radius: 0;
    transform: scale(1);
  }
}

.drop {
  position: absolute;
  left: 50%;
  top: 50%;

  height: 30px;
  width: 30px;
  background-color: pink;
  border-radius: 100%;
  animation: drop 1.5s;
  z-index: -2;
}

@keyframes drop {
  0% {
    opacity: 0.9;
    transform: translateY(500px);
  }
  50% {
    transform: translateY(-50px);
  }
  100% {
    opacity: 1;
    transform: translateY(0);
  }
}
</style>
