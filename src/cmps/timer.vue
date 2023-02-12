<template>
  <article
    class="count-down-timer"
    :class="[
      { red: startFrom <= startedRedColor && startFrom !== 0 },
      { blink: startFrom <= startedRedColor && startFrom !== 0 },
    ]"
  >
    {{ setTime }}
  </article>
</template>

<script>
export default {
  props: ['startFrom', 'toTime', 'onDone', 'startedRedColor'],
  watch: {
    startFrom(value) {
      if (value < 0) this.onDone()
    },
  },
  computed: {
    setTime() {
      let currTime = this.startFrom
      if (this.toTime) currTime = (this.toTime - new Date().getTime()) / 1000
      return currTime
    },
  },
}
</script>

<style lang="scss" scoped></style>
