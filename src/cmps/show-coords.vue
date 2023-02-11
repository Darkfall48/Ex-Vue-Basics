<template>
  <section>
    <h1>Take my coords</h1>
    <article class="mouse-monitor">
      <h1 class="mouse-monitor-title">Mouse Position</h1>
      <div className="mouse-monitor-pos">
        <h2 className="mouse-monitor-pos-x">
          X: <span>{{ pos.x }}</span>
        </h2>
        <h2 className="mouse-monitor-pos-y">
          Y: <span>{{ pos.y }}</span>
        </h2>
      </div>
      <button
        className="mouse-monitor-toggle-btn nice-button"
        v-on:click="handleToggle"
      >
        {{ isOn ? 'Pause' : 'Resume' }}
      </button>
    </article>
  </section>
</template>

<script>
export default {
  data() {
    return {
      isOn: true,
      pos: { x: 0, y: 0 },
    }
  },
  created() {
    document.addEventListener('mousemove', this.handleMouseMove)
  },
  unmounted() {
    document.removeEventListener('mousemove', this.handleMouseMove)
  },
  methods: {
    handleMouseMove(event) {
      this.pos = { x: event.clientX, y: event.clientY }
    },
    handleToggle() {
      this.isOn = !this.isOn
      if (this.isOn)
        document.addEventListener('mousemove', this.handleMouseMove)
      else document.removeEventListener('mousemove', this.handleMouseMove)
    },
  },
}
</script>

<style lang="scss" scoped>
.mouse-monitor {
  display: grid;
  gap: 8px;
  background-color: darkolivegreen;
  color: white;
  border-radius: 4px;
  padding: 18px;
  align-items: center;
  width: 200px;
  place-items: center;
  &-title {
  }
  &-pos {
    display: flex;
    flex-direction: row;
    justify-content: space-evenly;
    gap: 18px;
    &-x {
    }
    &-y {
    }
  }
  &-toggle-btn {
    margin-top: 16px;
    display: flex;
    place-content: center;
  }
}
</style>
