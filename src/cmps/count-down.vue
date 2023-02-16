<template>
  <section>
    <h1>County paradox!</h1>
    <section class="count-down">
      <Timer :startFrom="counter" @done="onDone" :startedRedColor="6" />
      <button @click="onStartTimer()" class="count-down-start-btn nice-button">
        Start
      </button>
      <button
        @click="onClearInterval()"
        class="count-down-pause-btn nice-button"
      >
        Pause
      </button>
      <button @click="onResetTimer()" class="count-down-reset-btn nice-button">
        Reset
      </button>
    </section>
  </section>
</template>

<script>
import Timer from './timer.vue'
export default {
  data() {
    return {
      audio: new Audio('/timer/timer.mp3'),
      isStarted: false,
      counter: 10,
      startedCounter: 10,
    }
  },
  methods: {
    onClearInterval() {
      clearInterval(this.intervalId)
      this.intervalId = null
    },
    onResetTimer() {
      this.onClearInterval()
      this.counter = this.startedCounter
    },
    onStartTimer() {
      if (this.intervalId) return
      this.intervalId = setInterval(this.onDecrease, 1000)
    },
    onDecrease() {
      this.counter--
    },
    onDone() {
      this.audio.play()
      this.onClearInterval()
      this.counter = 0
    },
  },
  components: { Timer },
}
</script>

<style lang="scss" scoped>
.count-down {
  background-color: darkorange;
  border-radius: 4px;
  padding: 18px;
  align-items: center;
  &-timer {
    color: darkmagenta;
    &.red {
      color: rgb(216, 71, 71);
    }
    &.blink {
      animation: blinker 1s linear infinite;
    }
    font-size: 32px;
    text-align: center;
    padding-bottom: 18px;
  }
  &-start-btn {
  }
  &-pause-btn {
  }
  &-reset-btn {
    margin-right: 0 !important;
  }
}

@keyframes blinker {
  50% {
    opacity: 0.6;
  }
}
</style>
