<template>
  <div>
    <img class="game-logo" alt="overlord logo" src="./assets/overlord.png">
    <OverlordGame msg="Welcome to Overlord Game"/>
  </div>
</template>

<script>
import OverlordGame from './components/OverlordGame.vue'

export default {
  name: 'App',
  components: {
    OverlordGame
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
  margin-top: 60px;
}
.game-logo {
  width: 15vw;
}
</style>
