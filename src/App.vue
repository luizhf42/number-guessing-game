<template>
  <main>
    <h1>Guess the number! 🐢</h1>
    <InitialScreen @gameStart="startTheGame" v-if="!gameHasStarted" />

    <GameScreen
      v-if="gameHasStarted"
      @resetGame="resetGame"
      :difficultyProp="difficulty"
    />
  </main>
</template>

<script>
import InitialScreen from "./components/InitialScreen.vue";
import GameScreen from "./components/GameScreen.vue";

export default {
  name: "App",
  components: {
    InitialScreen,
    GameScreen,
  },
  methods: {
    startTheGame({ difficulty, gameHasStarted }) {
      this.difficulty = difficulty;
      this.gameHasStarted = gameHasStarted;
    },
    resetGame() {
      this.gameHasStarted = false;
    },
  },
  data() {
    return {
      difficulty: "normal",
      gameHasStarted: false,
    };
  },
};
</script>