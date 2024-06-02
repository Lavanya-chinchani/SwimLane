<template>
  <div id="app">
    <div class="center-container">
      <SwimLane :lanes="lanes" />
    </div>
  </div>
</template>

<script>
import SwimLane from './components/SwimLane.vue'

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
          cards: [
            { imageUrl: 'https://i.pinimg.com/originals/bf/44/a7/bf44a7b492a2ea311a8cfa388c9fac2f.jpg' },
            { imageUrl: 'https://i.pinimg.com/originals/f9/41/50/f941508b4360fb06b67c351ce088b05f.jpg' },
            { imageUrl: 'https://i.pinimg.com/originals/58/25/1f/58251fcd7ddd69ad4d03e6df93743b14.jpg' },
            { imageUrl: 'https://i.pinimg.com/originals/26/46/34/264634bfda58d538c2a3d0836f3fb4e7.jpg' },
            { imageUrl: 'https://i.pinimg.com/originals/fd/9c/50/fd9c50dc04fd7de722e821ed545d40ac.jpg' },
            { imageUrl: 'https://i.pinimg.com/originals/f1/02/73/f10273e4b624a88a7af35810dc127d9f.jpg' },
            { imageUrl: 'https://i.pinimg.com/originals/75/b4/b1/75b4b10b8a1ff39f542adbe31ec5cd82.jpg' },
            { imageUrl: 'https://i.pinimg.com/originals/7c/36/b5/7c36b5c072dcf93ee2ba5f643cea83f0.jpg' },
            { imageUrl: 'https://i.pinimg.com/originals/15/38/28/153828c01b17e26b46d6188a0ff72e7b.jpg' },
            { imageUrl: 'https://i.pinimg.com/originals/02/71/e8/0271e8bb9a3c7b4c33876b955f2afa40.jpg' },
            { imageUrl: 'https://i.pinimg.com/originals/d2/8a/e8/d28ae893ce6f7237d7bbbf4fb43b9fde.jpg' }
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
  color: #2c3e50;
  background: url('https://media1.tenor.com/m/bOEs1oMtzcEAAAAC/charmie-anime-charmie-couple.gif') no-repeat center center fixed;
  background-size: cover; /* Ensures the GIF covers the entire background */
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 0; /* Reset margins */
}

.center-container {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 100%; /* Ensure it takes full height of the viewport */

}
</style>
