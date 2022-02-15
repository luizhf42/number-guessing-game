<template>
  <main>
    <h1>Guess the number! 🐢</h1>
    <InitialScreen />
    <!-- {gameHasStarted && (
    <GameScreen
      maximumNumber="{inputMaximumNumber}"
      chances="{chances}"
      randomNumber="{randomNumber}"
    />
    )} -->
  </main>
</template>

<script>
import InitialScreen from "./components/InitialScreen.vue";
export default {
  name: "App",
  components: {
    InitialScreen,
  },
  
};
</script>