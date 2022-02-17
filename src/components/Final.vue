<template>
  <div class="final">
    <div class="good-ending" v-if="userWon">
      <p>
        Great! You win! <br />
        The Turtle is happy for you.
      </p>
      <img
        class="turtle happy"
        src="../assets/turtle.png"
        alt="Happy turtle emoji"
      />
    </div>

    <div class="bad-ending" v-if="!userWon">
      <p>
        The Turtle was rooting for you and you lost. <br />
        The Turtle won't forget this.
      </p>
      <img
        class="turtle"
        src="../assets/sad-turtle.png"
        alt="Sad turtle emoji"
      />
    </div>
    <Button
      text="Play again! 🐢"
      :gameHasFinishedProp="gameHasFinished"
      @resetGame="this.$emit('resetGame')"
    />
  </div>
</template>

<script>
import Button from "./Button.vue";
export default {
  name: "Final",
  components: {
    Button,
  },
  props: {
    userWon: Boolean,
  },
  data() {
    return { gameHasFinished: true };
  },
  // methods() {
  //   resetGame() {
  //     this.$emit("resetGame")
  //   }
  // }
};
</script>

<style lang="scss" scoped>
.final {
  p {
    font-size: 1.15rem;
    font-weight: 700;
    width: 90%;
    margin: 10px auto 0;
  }
  .turtle {
    width: 55%;
    &.happy {
      animation: dance 1.3s infinite;
    }
  }
}

@keyframes dance {
  0%,
  100% {
    transform: rotateY(0);
  }

  50% {
    transform: rotateY(180deg);
  }
}
</style>