<template>
  <div class='row'>
    <b-modal
      class='text-center'
      hide-backdrop
      size='sm'
      title='Sound is ON'
      v-model='showAlert'
      :body-text-variant='bodyTextVariant'
      :hide-footer=true
      :hide-header=true
    >
      <div class='timer-alert' v-html='alertMessage'></div>
    </b-modal>
  </div>
</template>

<script>
// Ref: https://bootstrap-vue.js.org/docs/components/alert
// import bAlert from 'bootstrap-vue/es/components/alert/alert'
import { BModal } from 'bootstrap-vue';

export default {
  name: 'ToggleAlert',
  components: {
    BModal,
  },

  // variables
  data () {
    return {
      alertMessage: 'Autostart Next Interval is OFF',
      showAlert: false,
      bodyTextVariant: 'dark'
    }
  },
  computed: {
    isAutostartOn () {
      return this.$store ? this.$store.getters.isAutostartOn : false
    },
    soundIsOn () {
      return this.$store ? this.$store.state.soundIsOn : false
    }
  },
  watch: {
    isAutostartOn: function () {
      this.alertMessage = 'Autostart Next Interval is <span class="badge badge-' +
                          (this.isAutostartOn ? 'success">On' : 'danger">Off') +
                          '</span>'
      this.showAlert = true
    },
    soundIsOn: function () {
      this.alertMessage = 'Sound is <span class="badge badge-' +
                          (this.soundIsOn ? 'success">On' : 'danger">Off') +
                          '</span>'
      this.showAlert = true
    },
    showAlert: function (data) {
      if (data === true) {
        // Autoclose alert
        setTimeout(() => {
          this.showAlert = false
        }, 1000)
      }
    }
  },
  methods: {
  },
  mounted () {
  }
}
</script>

<!-- Unfortunately "scoped" cannot be applied to dynamic content
     Add .timer-alert class to minimize impact -->
<style>
.timer-alert .badge {
  font-weight: 400;
  font-size: 1rem;
}
</style>