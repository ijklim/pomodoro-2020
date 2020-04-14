<template>
  <div class='col-12 col-sm-10 col-md-8 mx-auto'>
    <button
      @click='click'
      class='btn btn-lg btn-block'
      v-html='buttonText()'
      v-bind:class="{
        'btn-success': this.$store && !this.$store.getters.isTimerOn && !this.$store.getters.isIntervalCompleted,
        'btn-light': this.$store && !this.$store.getters.isTimerOn && this.$store.getters.isIntervalCompleted,
        'btn-warning': this.$store && this.$store.getters.isTimerOn
      }"
      :disabled='this.$store && !this.$store.getters.isTimerOn && this.$store.getters.isIntervalCompleted'
    ></button>
  </div>
</template>

<script>
export default {
  // PascalCase, e.g. ThisIsAnExample
  name: 'TimerButton',

  // variables
  data () {
    return {
    }
  },
  methods: {
    buttonText (store = this.$store) {
      // Note: converted from computed to methods to allow store to be injected for unit testing purpose
      let text = '...'
      let currentIntervalIndex = store ? store.state.currentIntervalIndex : 0
      let pomodoroIntervals = store ? store.state.pomodoroIntervals : []
      let intervalName = store ? pomodoroIntervals[currentIntervalIndex].name : []
      let svg = false

      const VIEWPORT_DIMENSION = 30;    // Affects top left of SVG graphics
      const SVG_PLAY = `<svg width="${VIEWPORT_DIMENSION}" height="${VIEWPORT_DIMENSION}" viewBox="0 0 ${VIEWPORT_DIMENSION} ${VIEWPORT_DIMENSION}" fill="currentColor" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">` +
                       `<polygon points="5,2 19,11 5,19 5,2"></polygon>` +
                       `</svg>`
      const SVG_PAUSE = `<svg width="${VIEWPORT_DIMENSION}" height="${VIEWPORT_DIMENSION}" viewBox="0 0 ${VIEWPORT_DIMENSION} ${VIEWPORT_DIMENSION}" fill="currentColor" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">` +
                        `<rect x="6" y="2" width="4" height="16"></rect>` +
                        `<rect x="14" y="2" width="4" height="16"></rect>` +
                        `</svg>`
      const SVG_CHECK_SQUARE = `<svg width="${VIEWPORT_DIMENSION}" height="${VIEWPORT_DIMENSION}" viewBox="0 0 ${VIEWPORT_DIMENSION} ${VIEWPORT_DIMENSION}" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">` +
                               `<polyline points="9,10 12,13 23,1"></polyline>` +
                               `<path d="m21,12 v5 a2,2 0,0 1,-2 2 H5 a2,2 0,0 1,-2 -2 V3 a2,2 0,0 1,2 -2 h11"></path>` +
                               `</svg>`

      if (store) {
        if (store.getters.isIntervalCompleted) {
          text = `${intervalName} is completed`
          svg = SVG_CHECK_SQUARE
        } else if (store.getters.isTimerOn) {
          text = `Pause ${intervalName}`
          svg = SVG_PAUSE
        } else if (store.state.timer < pomodoroIntervals[currentIntervalIndex].time) {
          text = `Resume ${intervalName}`
          svg = SVG_PLAY
        } else {
          text = `Start ${intervalName}`
          svg = SVG_PLAY
        }
        if (svg) {
          text = `${svg} &nbsp;${text}`
        }
      }
      return text
    },
    click () {
      this.$store.commit('toggleTimer')
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>