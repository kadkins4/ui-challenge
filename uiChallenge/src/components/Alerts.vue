<template>
  <div class="alertsContainer">
    <div class="main">
        <div class="headerItem alertIdHeader">AlertID</div>
        <div class="headerItem alertTimeHeader">AlertTime</div>
        <div class="headerItem severityHeader">Severity</div>
        <div class="headerItem clientIpHeader">ClientIP</div>
        <div class="headerItem serverIpHeader">ServerIp</div>
        <div class="headerItem protocolHeader">Protocol</div>
        <div class="headerItem clientCountryHeader">ClientCountry</div>
    </div>
    <div>
      <!-- esline-disable-next-line -->
      <template v-if="info">
        <app-alert
          v-for="item in info"
          :alert="item"
          :key="item.AlertId"
        ></app-alert>
      </template>
      <template v-else>
        <p>No Data To Display</p>
      </template>
    </div>
  </div>
</template>

<script>
import { bus } from '../main.js'
import Alert from './Alert.vue'
// @cleanup: local import not working with fetch for some reason
// import alertsJson from '../resource/alerts.json'
export default {
  data () {
    return {
      // main data
      info: null,
      high: 0,
      med: 0,
      low: 0
    }
  },
  components: {
    appAlert: Alert
  },
  beforeCreate () {
    // context
    var self = this
    fetch('https://raw.githubusercontent.com/fidelisui/ui-challenge/master/alerts.json')
      .then(function (response) {
        if (response.status !== 200) {
          console.log('Error Code: ' + response.status)
          return
        }
        // set info to retrieved data
        response.json().then(function (data) {
          self.info = data
        })
      })
      .catch(function (err) {
        console.log('Error: ', err)
      })
  },
  methods: {
    incHigh () {
      this.high += 1
      console.log('High:', this.high)
    },
    incMed () {
      this.med += 1
      console.log('Med:', this.med)
    },
    incLow () {
      this.low += 1
      console.log('Low:', this.low)
    }
  },
  // trigger everytime info changes.
  // doing on this component to catch every time it changes,
  // as if it were going to change live.
  watch: {
    info () {
      // create statistics
      let data = this.info
      data.forEach(el => {
        // Severity Calculation
        if (el.Severity === 'High') this.incHigh()
        if (el.Severity === 'Medium') this.incMed()
        if (el.Severity === 'Low') this.incLow()
      })
      bus.$emit('createStats', this)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.alertsContainer {
  display: flex;
  flex-direction: column;
}

.main {
  display: grid;
  grid-template-columns: 14;
  grid-template-rows: 2;
  padding: 5px 5px 5px 0;
  width: 950px;
  background: lightslategray;
}

.headerItem {
  grid-row-start: 1;
  grid-row-end: 1;
  font-weight: 700;
}

.alertIdHeader {
  grid-column-start: 1;
  grid-column-end: 2;
  text-align: left;
}

.alertTimeHeader {
  grid-column-start: 2;
  grid-column-end: 4;
}

.severityHeader {
  grid-column-start: 5;
  grid-column-end: 7;
}

.clientIpHeader {
  grid-column-start: 7;
  grid-column-end: 9;
}

.serverIpHeader {
  grid-column-start: 9;
  grid-column-end: 11;
}

.protocolHeader {
  grid-column-start: 11;
  grid-column-end: 13;
}

.clientCountryHeader {
  grid-column-start: 13;
  grid-column-end: 15;
}
</style>
