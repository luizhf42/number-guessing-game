<template>
  <section class="game" @load="setGameConfigs">
    <h2 :style="[gameHasFinished ? 'text-decoration: line-through' : '']">
      Choose a number between 1 and {{ this.maximumNumber }}
    </h2>

    <form @submit="checkGuess($event)">
      <input
        :readonly="gameHasFinished"
        autocomplete="off"
        v-model="guess"
        type="number"
        id="input"
        min="1"
        :max="maximumNumber"
        placeholder="Glory number"
      />
      <div class="btn-container" v-if="!gameHasFinished">
        <Button text="Guesstimate!" :gameHasFinished="gameHasFinished" />
      </div>
    </form>

    <p v-if="this.remainingChances">
      Remaining chances: {{ remainingChances }}
    </p>

    <p class="message" v-show="showMessage">{{ message }}</p>

    <Final
      v-if="gameHasFinished"
      :userWon="this.userWon"
      @resetGame="this.$emit('resetGame')"
    />
  </section>
</template>

<script>
import anime from "animejs";
import Button from "./Button.vue";
import Final from "./Final.vue";

export default {
  name: "GameScreen",
  components: {
    Final,
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
      randomNumber: 0,
      message: "",
      showMessage: false,
      gameHasFinished: false,
      userWon: false,
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
    this.randomNumber = this.randomizeNumber();
  },
  methods: {
    checkGuess(event) {
      event.preventDefault();
      const guess = this.guess;
      const randomNumber = this.randomNumber;
      if (guess) {
        if (this.remainingChances) {
          if (guess == randomNumber) {
            this.message = `Congratulations! The random number was ${randomNumber}!`;
            this.gameHasFinished = true;
            this.remainingChances = 0;
            this.userWon = true;
          } else if (guess != randomNumber && this.remainingChances <= 1) {
            this.message = `Your guess was wrong and the chances are over. You lose! The random number was ${randomNumber}.`;
            this.gameHasFinished = true;
            this.remainingChances--;
          } else if (guess > randomNumber) {
            this.message = `Your guess (${guess}) was too high! Try again.`;
            this.remainingChances--;
          } else if (guess < randomNumber) {
            this.message = `Your guess (${guess}) was too low! Try again.`;
            this.remainingChances--;
          }
        }

        this.showMessage = true;
        if (!this.gameHasFinished) this.guess = "";
      } else {
        anime({
          targets: "#input",
          easing: "easeInOutSine",
          duration: 550,
          translateX: [
            {
              value: -16,
            },
            {
              value: 16,
            },
            {
              value: -8,
            },
            {
              value: 8,
            },
            {
              value: 0,
            },
          ],
        });
      }
    },

    randomizeNumber() {
      const randomNumber = Math.round(Math.random() * this.maximumNumber);
      return randomNumber;
    },
  },
};
</script>

<style lang="scss" scoped>
@use "../App.scss";

$input-border: 1px solid App.$input-border;

.game {
  width: 100%;
  @include App.flex();
  gap: 12px;

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
        color: #5d875d;
      }
    }

    .btn-container {
      @extend .game;
    }
  }

  h2 {
    margin-bottom: 0 !important;
  }

  .message {
    // font-weight: 700;
    font-size: 1.1rem;
  }
}
</style>