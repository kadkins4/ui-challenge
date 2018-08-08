<template>
    <!-- Header Component -->
    <div class="header">
        <!-- give header grid of 14 columns, 1 row -->
        <div class="btnContainer">
            <!-- 1 div = 1 column -->
            <!-- Make buttons separate component, if does something -->
            <button
                class="active"
                @click="clicked">Alerts</button>
        </div>
        <div class="btnContainer">
            <button
                class="inactive"
                @click="clicked">Events</button>
        </div>
    </div>
</template>

<script>
export default {
  data () {
    return {
      // no data needed in this case
    }
  },
  methods: {
    // nothing happens
    clicked () {
      console.log('you\'ve clicked a button which does nothing.')
    }
  }
}
</script>

<style>
  .header {
    height: 50px;
    display: flex;
    flex-direction: row;
    justify-content: flex-start;
    align-items: center;
    background: darkgray;
  }

  .btnContainer {
    margin: auto 20px;
  }

  button {
    padding: 10px 20px;
    font-weight: 700;
    font-size: 15px;
  }

  .active {
    background: white;
    color: black;
  }

  .inactive {
    background: transparent;
    color: white;
    border: none;
  }
</style>
