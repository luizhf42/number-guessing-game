<template>
  <button @click="buttonClick()">{{ text }}</button>
</template>

<script>
export default {
  name: "Button",
  props: {
    text: String,
    gameHasStartedProp: Boolean,
    gameHasFinishedProp: Boolean,
  },
  data() {
    return {
      gameHasStarted: this.gameHasStartedProp,
      gameHasFinished: this.gameHasFinishedProp,
    };
  },
  methods: {
    buttonClick() {
      if (!this.gameHasStarted) {
        this.gameHasStarted = true;
        this.$emit("gameStart", this.gameHasStarted);
      }
      if (this.gameHasFinished) {
        this.$emit("resetGame");
      }
    },
  },
};
</script>

<style lang="scss" scoped>
@use "../App.scss";

button {
  cursor: pointer;
  border: 0;
  background: App.$button;
  color: App.$main-bg;
  width: 50%;
  padding: 10px;
  font-weight: 700;
  font-size: 1.1rem;
  border-radius: 5px;
  transition: 0.3s;

  &:hover {
    background: App.$button-hover;
  }
  // &:disabled {
  //   background: App.$button-disabled;
  //   cursor: default;
  // }
}
</style>