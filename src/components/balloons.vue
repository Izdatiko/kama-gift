<template>
  <div id="balloon-container" ref="balloonContainer"></div>
</template>

<script setup>
import Home from '@/views/home.vue';
import { ref, onMounted, onBeforeUnmount } from 'vue';
import { useRouter, useRoute } from 'vue-router'

const balloonContainer = ref(null);


const router = useRouter()

function random(num) {
  return Math.floor(Math.random() * num);
}

function getRandomStyles() {
  const r = random(255);
  const g = random(255);
  const b = random(255);
  const mt = random(200);
  const ml = random(50);
  const dur = random(5) + 5;
  return `
    background-color: rgba(${r},${g},${b},0.7);
    color: rgba(${r},${g},${b},0.7); 
    box-shadow: inset -7px -3px 10px rgba(${r - 10},${g - 10},${b - 10},0.7);
    margin: ${mt}px 0 0 ${ml}px;
    animation: float ${dur}s linear infinite; /* Apply the float animation */
  `;
}

function createBalloons(num) {
  for (let i = 0; i < num; i++) {
    const balloon = document.createElement("div");
    balloon.className = "balloon";
    balloon.style.cssText = getRandomStyles();
    balloonContainer.value.append(balloon);
  }
}

function removeBalloons() {
  event.preventDefault();
  balloonContainer.value.style.opacity = 0;
  setTimeout(() => {
    balloonContainer.value.remove();
  }, 500);
  router.push({name: 'home'})
}

onMounted(() => {
  createBalloons(30);
  
  const router = useRouter()
  window.addEventListener("click", removeBalloons);
  window.addEventListener("touchstart", removeBalloons);
});

onBeforeUnmount(() => {
  window.removeEventListener("click", removeBalloons);
});
</script>

<style>
body {
  margin: 0;
}

#balloon-container {
  height: 100vh;
  padding: 1em;
  box-sizing: border-box;
  display: flex;
  flex-wrap: wrap;
  overflow: hidden;
  transition: opacity 500ms;
}

.balloon {
  height: 125px;
  width: 105px;
  border-radius: 75% 75% 70% 70%;
  position: relative;
}

.balloon:before {
  content: "";
  height: 75px;
  width: 1px;
  background-color: #FDFD96;
  display: block;
  position: absolute;
  top: 125px;
  left: 0;
  right: 0;
  margin: auto;
}

.balloon:after {
  content: "▲";
  text-align: center;
  display: block;
  position: absolute;
  color: inherit;
  top: 120px;
  left: 0;
  right: 0;
  margin: auto;
}

@keyframes float {
  from { transform: translateY(0); opacity: 1; }
  to { transform: translateY(-100vh); opacity: 0; } /* Move upwards */
}
</style>
