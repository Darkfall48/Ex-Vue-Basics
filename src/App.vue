<script setup>
import { ref } from 'vue'

import ShowTime from '@/cmps/show-time.vue'
import CountDown from '@/cmps/count-down.vue'
import WhoWatch from '@/cmps/who-watch.vue'
import ShowCoords from '@/cmps/show-coords.vue'

const route = ref('count down')
</script>

<template>
  <header class="main-nav">
    <button v-on:click="route = 'show time'">Show Time</button>
    <button v-on:click="route = 'count down'">Count Down</button>
    <button v-on:click="route = 'watcher'">Who's Watch ?</button>
    <button v-on:click="route = 'mouse coords'">Mouse Coords</button>
  </header>

  <main class="main-cmps">
    <ShowTime v-if="route === 'show time'" />
    <CountDown v-if="route === 'count down'" />
    <WhoWatch v-if="route === 'watcher'" />
    <ShowCoords v-if="route === 'mouse coords'" />
  </main>
</template>

<style lang="scss">
.main {
  &-nav {
    display: flex;
    flex-direction: row;
    gap: 18px;
    place-content: center;
  }
  &-cmps {
    display: flex;
    flex-direction: column;
    place-content: center;
    place-items: center;
  }
}
</style>
