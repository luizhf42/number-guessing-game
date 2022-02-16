<template>
  <section class="game" @load="setGameConfigs">
    <h2>Choose a number between 1 and {{ this.maximumNumber }}</h2>

    <form>
      <input
        v-model="guess"
        type="number"
        id="input"
        min="1"
        :max="maximumNumber"
        placeholder="Glory number"
      />
      <Button text="Guesstimate!" />
    </form>

    <p>Remaining chances: {{ remainingChances }}</p>

    <!-- {showResult && (
    <Result guessResult="{guessResult}" submittedGuess="{submittedGuess}" />
    )} -->
  </section>
</template>

<script>
import Button from "./Button.vue";
export default {
  name: "GameScreen",
  components: {
    Button,
  },
  props: {
    difficultyProp: String,
  },
  data() {
    return {
      difficulty: this.difficultyProp,
      maximumNumber: 50,
      remainingChances: 0,
      guess: "",
    };
  },
  mounted() {
    switch (this.difficulty) {
      case "very-easy":
        this.maximumNumber = 10;
        this.remainingChances = 3;
        break;
      case "easy":
        this.maximumNumber = 20;
        this.remainingChances = 3;
        break;
      case "normal":
        this.maximumNumber = 50;
        this.remainingChances = 4;
        break;
      case "hard":
        this.maximumNumber = 100;
        this.remainingChances = 4;
        break;
      case "very-hard":
        this.maximumNumber = 1000;
        this.remainingChances = 6;
        break;
    }
  },
};
</script>

<style lang="scss" scoped>
@use "../App.scss";

$input-border: 1px solid App.$input-border;

.game {
  width: 100%;
  @include App.flex();
  gap: 10px;

  form {
    @extend .game;
    input {
      background: transparent;
      border: $input-border;
      border-radius: 5px;
      width: 40%;
      padding: 5px 7px;

      &:focus {
        outline: $input-border;
      }
      &::placeholder {
        font-family: inherit;
      }
    }
  }
}
</style>