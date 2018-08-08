<template>
  <div class="homeContainer">
      <!-- HEADER component from App.Vue -->

      <!-- STATS component -->
      <app-stats></app-stats>
      <!-- ALERTS component, child is ALERT component -->
      <app-alerts></app-alerts>

      <!-- ALERTDETAIL component -->
      <app-alert-detail></app-alert-detail>
  </div>
</template>

<script>
import Header from './Header.vue'
import Alerts from './Alerts.vue'
import AlertDetail from './AlertDetail.vue'
import Stats from './Stats.vue'

export default {
  data () {
    return {

    }
  },
  components: {
    appHeader: Header,
    appAlerts: Alerts,
    appAlertDetail: AlertDetail,
    appStats: Stats
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .homeContainer {
    display: flex;
    flex-direction: row;
  }
</style>
