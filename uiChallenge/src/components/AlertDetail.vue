<template>
  <div class="alertDetailContainer">
    <h3>Alert Details: <span v-show="AlertId"> {{ AlertId }} </span></h3>
    <template v-if="AlertId">
      <div class="detail">
        <div class="lineItem">
          <p>Alert ID:</p>
          <p>{{ AlertId }}</p>
        </div>
        <div class="lineItem">
          <p>Alert Time:</p>
          <p>{{ AlertTime }}</p>
        </div>
        <div class="lineItem">
          <p>Severity:</p>
          <p>{{ Severity }}</p>
        </div>
        <div class="lineItem">
          <p>ClientIP:</p>
          <p>{{ ClientIP }}</p>
        </div>
        <div class="lineItem">
          <p>ServerIP:</p>
          <p>{{ ServerIP }}</p>
        </div>
        <div class="lineItem">
          <p>Protocol:</p>
          <p>{{ Protocol }}</p>
        </div>
        <div class="lineItem">
          <p>ClientCountry:</p>
          <p>{{ ClientCountry }}</p>
        </div>
      </div>
    </template>
    <template v-else>
      <div class="detail">
        <p class="noAlert">No Alert Has Been Selected.</p>
      </div>
    </template>
  </div>
</template>

<script>
import { bus } from '../main.js'

export default {
  data () {
    return {
      // main data
      AlertId: null,
      AlertTime: null,
      Severity: null,
      ClientIP: null,
      ServerIP: null,
      Protocol: null,
      ClientCountry: null
    }
  },
  created () {
    bus.$on('toggleAlert', (selection) => {
      // use selection to populate data
      if (selection.AlertId !== this.AlertId) {
        this.AlertId = selection.AlertId
        this.AlertTime = selection.AlertTime
        this.Severity = selection.Severity
        this.ClientIP = selection.ClientIP
        this.ServerIP = selection.ServerIP
        this.Protocol = selection.Protocol
        this.ClientCountry = selection.ClientCountry
      }
    })
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .noAlert {
    color: green;
    text-align: center;
  }

  .detail {
    display: flex;
    flex-direction: column;
    padding: 25px 10px 0 10px;
  }

  .lineItem {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
  }
</style>
