<template>
  <div class="initial-screen" v-if="!gameHasStarted">
    <h2>Choose the difficulty</h2>
    <div class="difficulties">
      <label>
        <input type="radio" name="difficulty" id="very-easy" />
        <span class="checkmark"></span> Very Easy
      </label>
      <label>
        <input type="radio" name="difficulty" id="easy" />
        <span class="checkmark"></span> Easy
      </label>
      <label>
        <input type="radio" name="difficulty" id="normal" />
        <span class="checkmark"></span> Normal
      </label>
      <label>
        <input type="radio" name="difficulty" id="hard" />
        <span class="checkmark"></span> Hard
      </label>
      <label>
        <input type="radio" name="difficulty" id="very-hard" />
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
</template>

<script>
export default {
  name: "InitialScreen",
};
</script>

<style>
</style>