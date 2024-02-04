<script setup>
import lottie from "lottie-web";
import { ref, onMounted } from "vue";
import animationData from "./assets/lottie-test11.json";
import { useScroll } from "@vueuse/core";

const elBox = ref();
const { x, y } = useScroll(elBox);

const loadLottie = () => {
  lottie.loadAnimation({
    container: document.getElementById("lottie-box"), // the dom element that will contain the animation
    renderer: "svg",
    loop: false,
    autoplay: false,
    animationData: animationData, // the path to the animation json
  });
};

const onScroll = () => {
  if (y.value > 100) {
    lottie.play();
    console.log("play");
  }
};

onMounted(() => {
  loadLottie();
});
</script>

<template>
  <div class="wrapper" ref="elBox" @scroll="onScroll()">
    <div class="box"></div>
    <div class="box">
      <div class="main-box" :class="{ 'big-box': y !== 0 }">
        <div id="lottie-box" style="width: 500px; height: 500px"></div>
        {{ x }} / {{ y }}
      </div>
    </div>
    <div class="box"></div>
    <div class="box"></div>
    <div class="box"></div>
    <div class="box"></div>
    <div class="box"></div>
  </div>
</template>

<style scoped>
.wrapper {
  width: 100vw;
  height: 100vh;
  overflow-y: scroll;
}
.box {
  width: 100vw;
  height: 600px;
  display: flex;
  justify-content: center;
  align-items: center;

  .main-box {
    background-color: #171b20;
    border-radius: 30px;
    width: 600px;
    height: 400px;
    display: flex;
    justify-content: center;
    align-items: center;

    &.big-box {
      width: 100vh;
      height: 100%;
    }
  }
}
</style>
