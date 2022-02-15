<template>
  <div class="initial-screen" v-if="!gameHasStarted">
    <h2>Choose the difficulty</h2>
    <div class="difficulties">
      <label id="oi">
        <input
          @click="changeDifficulty($event)"
          type="radio"
          name="difficulty"
          id="very-easy"
        />
        <span class="checkmark"></span> Very Easy
      </label>
      <label>
        <input
          @click="changeDifficulty($event)"
          type="radio"
          name="difficulty"
          id="easy"
        />
        <span class="checkmark"></span> Easy
      </label>
      <label>
        <input
          @click="changeDifficulty($event)"
          type="radio"
          name="difficulty"
          id="normal"
          checked
        />
        <span class="checkmark"></span> Normal
      </label>
      <label>
        <input
          @click="changeDifficulty($event)"
          type="radio"
          name="difficulty"
          id="hard"
        />
        <span class="checkmark"></span> Hard
      </label>
      <label>
        <input
          @click="changeDifficulty($event)"
          type="radio"
          name="difficulty"
          id="very-hard"
        />
        <span class="checkmark"></span> Impossible
      </label>
    </div>
    <h2>
      Play with a random number between 1 and
      <span v-if="difficulty == 'very-easy'">10</span>
      <span v-if="difficulty == 'easy'">20</span>
      <span v-if="difficulty == 'normal'">50</span>
      <span v-if="difficulty == 'hard'">100</span>
      <span v-if="difficulty == 'very-hard'">1000</span>
    </h2>
    <!-- <Button
        text="Start the game!"
        gameHasStarted="{gameHasStarted}"
        setGameHasStarted="{setGameHasStarted}"
        startTheGame="{startTheGame}"
      /> -->
  </div>
  <Button text="Start the game!" :gameHasStarted="gameHasStarted" />
</template>

<script>
import Button from "./Button.vue";
export default {
  name: "InitialScreen",
  components: {
    Button,
  },
  methods: {
    changeDifficulty(event) {
      this.difficulty = event.target.id;
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

<style lang="scss" scoped>
@use "../App.scss";

.initial-screen {
  width: 100%;
  margin: 4px 0;
  .difficulties {
    margin: 6px auto 12px;
    width: 90%;
    @include App.flex(row, space-evenly);
    flex-wrap: wrap;
    gap: 3px;

    label {
      @include App.flex(row);
      position: relative;
      margin-bottom: 5px;

      input {
        position: absolute;
        opacity: 0;
        cursor: pointer;
        height: 0;
        width: 0;

        &:checked ~ .checkmark {
          background-color: App.$checkmark-checked;

          &:after {
            display: block;
          }
        }
      }

      .checkmark {
        transition: 0.3s;
        display: inline-block;
        height: 18px;
        width: 18px;
        background-color: App.$checkmark;
        border-radius: 50%;
        margin-right: 3px;

        &:after {
          content: "";
          position: absolute;
          display: none;
          top: 6px;
          left: 6px;
          width: 6px;
          height: 6px;
          border-radius: 50%;
          background: white;
        }
      }

      &:hover input:not(:checked) ~ .checkmark {
        background-color: App.$checkmark-hover;
      }
    }
  }
}
</style>