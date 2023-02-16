<template>
  <section class="challenge-section">
    <h1>It's Show Time!</h1>
    <section
      v-on:click="handleClick"
      :class="{ 'season-clock': true, dark: isDark }"
      :title="[isDark ? 'Change to Dark' : ' Change to Light']"
    >
      <article class="season-clock-title">
        {{ currMonth }} <span>({{ currSeason }})</span>
      </article>
      <img v-bind:src="imgUrl" v-bind:alt="currSeason" />
      <article class="season-clock-day">{{ currDay }}</article>
      <article class="season-clock-time">
        {{ currHour + ':' + currMinute }}
      </article>
    </section>
  </section>
</template>

<script>
import { utilService } from '@/assets/services/util.service.js'
export default {
  data() {
    return {
      clock: new Date(),
      //   currSeason: '',
      //   currMonth: '',
      //   currDay: '',
      //   currHour: null,
      //   currMinute: null,
      imgUrl: `public/imgs/seasons/seasons.png`,
      isDark: false,
    }
  },
  created() {
    this.interval = setInterval(() => {
      this.clock = new Date()
      // console.log('Clock', this.clock)
    }, 1000)
    this.currSeason = utilService.getSeason(this.clock)
    this.currMonth = utilService.getMonthName(this.clock)
    this.currDay = utilService.getDayName(this.clock)
    this.currHour = this.clock.getHours()
    this.currMinute = this.clock.getMinutes()
    this.imgUrl = `public/imgs/seasons/${this.currSeason.toLocaleLowerCase()}.png`
    //? For Debug:
    // this.imgUrl = `/imgs/seasons/winter.png`
    // this.imgUrl = `/imgs/seasons/autumn.png`
    // this.imgUrl = `/imgs/seasons/spring.png`
    // this.imgUrl = `/imgs/seasons/summer.png`
  },
  unmounted() {
    clearInterval(this.interval)
  },
  methods: {
    handleClick() {
      this.isDark = !this.isDark
    },
  },
  computed: {
    isDarkClass() {
      return 'season-clock' + this.isDark ? 'dark' : ''
    },
  },
}
</script>

<style lang="scss" scoped>
.season-clock {
  background-color: darkcyan;
  color: white;
  width: 480px;
  height: fit-content;
  text-align: center;
  padding: 18px;
  border-radius: 8px;
  cursor: pointer;
  &.dark {
    background-color: #333;
    color: white;
  }
  &-title {
    font-size: 48px;
  }
  &-day {
    font-size: 48px;
  }
  &-time {
    font-size: 48px;
  }
}
</style>
