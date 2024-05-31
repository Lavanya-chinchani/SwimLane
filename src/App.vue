<template>
    <div id="app">
      <SwimLane :lanes="lanes" />
    </div>
  </template>

<script>
import SwimLane from './SwimLane.vue'

export default {
  name: 'App',
  components: {
    SwimLane
  },
  data () {
    return {
      lanes: [
        {
          id: 1,
          title: 'Single Large Lane',
          cards: [
            'Card 1', 'Card 2', 'Card 3', 'Card 4', 'Card 5',
            'Card 6', 'Card 7', 'Card 8', 'Card 9', 'Card 10'
          ],
          top: 0,
          left: 0,
          height: 0, // This will be set dynamically in SwimLane.vue
          width: 0 // This will be set dynamically in SwimLane.vue
        }
      ]
    }
  }
}
</script>

  <style>
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    margin-top: 60px;
  }
  </style>
