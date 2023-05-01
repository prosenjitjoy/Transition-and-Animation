<script setup lang="ts">
import { ref, onMounted } from 'vue';
import Animation1 from './components/Animation1.vue';
import { gsap } from 'gsap';

const msg = "Hello World!"
const show = ref(false)

const logo = ref()
const logo1 = ref()
const logo2 = ref()
onMounted(() => {
  // gsap.from(logo.value, { duration: 30, rotation: 3600 })
  // gsap.to(logo1.value, { duration: 4, scale: 1.2, rotation: '-=16', ease: 'elastic(2.5, 0.5)' })
  // gsap.to(logo2.value, 2, {
  //   duration: 2,
  //   scale: 0.1,
  //   y: 60,
  //   yoyo: true,
  //   repeat: 1,
  //   ease: "power3.inOut",
  //   delay: 1,
  //   stagger: {
  //     amount: 1.5,
  //     grid: "auto",
  //     from: "center",
  //     repeat: 5
  //   }
  // })

  const tl = gsap.timeline({ repeat: -1 })
  tl.from(logo.value, { duration: 5, rotation: 600 })
  tl.to(logo1.value, { duration: 4, scale: 1.2, rotation: '-=16', ease: 'elastic(2.5, 0.5)' }, "+=1")
  tl.to(logo2.value, 2, {
    duration: 2,
    scale: 0.1,
    y: 60,
    yoyo: true,
    repeat: 1,
    ease: "power3.inOut",
    delay: 1,
    stagger: {
      amount: 1.5,
      grid: "auto",
      from: "center",
    }
  }, "-=1")

  const tl1 = gsap.timeline({ defaults: { duration: 2 }, repeat: -1 })
  tl1.to("#box-green", { x: 550 }).to("#box-red", { scale: 0.5, x: 425 }, "+=1").to("#box-purple", { scale: 1.2, ease: "bounce", x: 500 }, "-=1")
})
</script>

<template>
  <div class="container">
    <button class="bg-gray-400 text-white px-5 py-2.5 rounded" @click="show = !show">Toggle</button>
    <Transition name="fade-in">
      <h1 v-show="show">{{ msg }}</h1>
    </Transition>
  </div>

  <div class="container">
    <Animation1 />
  </div>

  <img id="img" src="/vite.svg" alt="vite" ref="logo">
  <img id="img" src="/vite.svg" alt="vite" ref="logo1">
  <img id="img" src="/vite.svg" alt="vite" ref="logo2">

  <div class="my-8 flex gap-4">
    <div id="box-green" class="bg-green-500 w-12 h-12"></div>
    <div id="box-red" class="bg-red-500 w-12 h-12"></div>
    <div id="box-purple" class="bg-purple-500 w-12 h-12"></div>
  </div>
</template>



<style>
.fade-in-enter-from,
.fade-in-leave-to {
  opacity: 0;
}

.fade-in-enter-active,
.fade-in-leave-active {
  transition: opacity 2s ease-in;
}
</style>