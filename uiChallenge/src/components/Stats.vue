<template>
  <div class="statsContainer">
    <h3>Statistics</h3>
    <div>High: {{ high }}</div>
    <div>Med: {{ med }}</div>
    <div>Low: {{ low }}</div>
  </div>
</template>

<script>
import { bus } from '../main.js'

export default {
  data () {
    return {
      high: 0,
      med: 0,
      low: 0
    }
  },
  created () {
    bus.$on('createStats', (data) => {
      this.high = data.high
      this.med = data.med
      this.low = data.low
    })
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.statsContainer {
  width: 175px;
}

</style>
