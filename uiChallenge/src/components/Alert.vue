<template>
  <!-- on selection... highlight -->
  <div class="line"
    v-bind:class="{ selected: isSelected }"
    @click="toggleSelect">
    <!-- Add toggle select on individual alert... use event bus to
    get the state back to Alert Details and clear out any other -->
      <div class="alertId"> {{ AlertId }} </div>
      <div class="alertTime"> {{ AlertTime }} </div>
      <!-- color calculated on severity -->
      <div
        class="severity"
        v-bind:class="color"
        > {{ Severity }} </div>
      <div class="clientIp"> {{ ClientIP }} </div>
      <div class="serverIp"> {{ ServerIP }} </div>
      <div class="protocol"> {{ Protocol }} </div>
      <div class="clientCountry"> {{ ClientCountry }} </div>
  </div>
</template>

<script>
import { bus } from '../main.js'

export default {
  props: ['alert'],
  data () {
    return {
      isSelected: false,
      AlertId: this.alert.AlertId,
      AlertTime: this.alert.AlertTime,
      Severity: this.alert.Severity,
      ClientIP: this.alert.ClientIP,
      ServerIP: this.alert.ServerIP,
      Protocol: this.alert.Protocol,
      ClientCountry: this.alert.ClientCountry
    }
  },
  computed: {
    color () {
      // switch case for class
      let color = null
      switch (this.Severity) {
        case 'Low':
          color = 'green'
          break
        case 'Medium':
          color = 'yellow'
          break
        case 'High':
          color = 'red'
          break
        default:
        // something else was added and is 'flagged'
          color = 'black'
      }
      return color
    }
  },
  methods: {
    // emits action to bus --> other listeners
    toggleSelect () {
      bus.$emit('toggleAlert', this)
    }
  },
  created () {
  // listens for emit from bus
    bus.$on('toggleAlert', (selection) => {
      // sets isSelected property on each Alert
      this.isSelected = this.AlertId === selection.AlertId
    })
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
/* @cleanup !!!! manual css !!! change for bootstrap or Vuetify */
  .line {
      display: flex;
      flex-direction: row;
      align-content: flex-start;
      width: 950px;
      cursor: pointer;
  }

  /* if selected highlight, else show regular */
  .selected {
      background: lightblue;
  }

  .alertId {
      width: 120px;
      text-align: left;
  }

  .alertTime {
      width: 150px;
  }

  .severity {
      width: 90px;
      text-align: left;
      margin: 0 0 0 43px;
  }

  /* styling specific to severity */
  .green {
      color: green;
  }

  .yellow {
      color: rgb(202, 202, 44);
  }

  .red {
      color: red;
  }

  .black {
      color: black;
      background: red;
  }

  .clientIp {
      width: 120px;
      text-align: left;
  }

  .serverIp {
      margin: 0 0 0 30px;
      width: 120px;
      text-align: left;
  }

  .protocol {
      width: 40px;
      margin: 0 0 0 20px;
      text-align: left;
  }

  .clientCountry {
      margin: 0 0 0 80px;
      width: 100px;
      text-align: left;
  }
</style>
