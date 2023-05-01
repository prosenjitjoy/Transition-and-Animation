<script setup lang="ts">
import { ref, } from 'vue';
const message = ref("")
const textArea = ref("")
const onSendClick = () => {
  message.value = textArea.value
  textArea.value = ""
}

const messages = ref([
  "Hello, how are you?",
  "The weather is nice",
  "This is the message feed",
  "And I am the fourth message",
  "Chapter 8 is fun",
  "Animation is super awesome",
  "Sorry, I didn't know you called",
  "Be patient, animation comes right up",
])
let show = ref(false)
const showList = () => {
  show.value = !show.value
}
const sorting = (isDescending: boolean) => {
  messages.value.sort()
  if (isDescending) {
    messages.value.reverse()
  }
}

const shuffle = () => {
  messages.value.sort(() => Math.random() - 0.5)
}
</script>

<template>
  <div>
    <textarea cols="30" rows="3" class="block bg-gray-50 rounded shadow" v-model="textArea"></textarea>
    <button class="my-2 bg-gray-400 text-white rounded px-5 py-2.5" @click="onSendClick()">Submit</button>
  </div>

  <div>
    <Transition name="slide-right" enter-active-class="slide-right" leave-active-class="slide-left">
      <section v-if="message">
        <h4>Your saved message: </h4>
        <span>{{ message }}</span>
      </section>
    </Transition>
  </div>

  <div>
    <button class="my-2 bg-gray-400 text-white rounded px-5 py-2.5" @click="showList()">Show List</button>
    <TransitionGroup name="fade" move-class="fade-move-in">
      <p v-for="(message, index) in messages" :key="index" v-show="show">{{ message }}</p>
    </TransitionGroup>
  </div>

  <div>
    <button class="my-2 bg-gray-400 text-white rounded px-5 py-2.5 mr-2" @click="sorting(false)">Sort A-Z</button>
    <button class="my-2 bg-gray-400 text-white rounded px-5 py-2.5 mr-2" @click="sorting(true)">Sort Z-A</button>
    <button class="my-2 bg-gray-400 text-white rounded px-5 py-2.5 mr-2" @click="shuffle()">Shuffle</button>
    <TransitionGroup name="flip" tag="div" appear>

      <p class="message--item" v-for="(message, index) in messages" :key="index">
        {{ message }}
      </p>
    </TransitionGroup>
  </div>
</template>

<style>
@keyframes slide-right {
  100% {
    transform: translateX(0);
  }
}

.slide-right {
  animation: 1s slide-right 1s forwards;
  transform: translateX(-100%);
  transition: border-top 2s ease;
}

.slide-left {
  animation: 1s slide-right 1s reverse;
  transform: translateX(-100%);
}

.slide-right-enter-from {
  border-top: 0;
}

.fade-enter-active,
.fade-leave-active {
  transition: all 2s;
}

.fade-enter-from,
.fade-leave-active {
  opacity: 0;
  transform: translateX(30px);
}

.fade-move-in {
  transition: transform 2s ease-in;
}

.flip-enter-from,
.flip-leave-to {
  opacity: 0;
  transform: translateY(20px);
}

.message--item {
  transition: all 2s;
}

.flip-leave-active {
  position: absolute;
}

.flip-move {
  transition: transform 1s;
}
</style>