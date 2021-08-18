<template>
  <h1>Reaction Timer</h1>
  <div class="info">
    How to play : wait until a box appeared then quickly click on it
  </div>
  <button
    @click="toggleIsPlaying"
    :disabled="isPlaying"
  >
    play
  </button>

  <div
    v-if="result&&result!==7000"
    class="score"
  >
    score: {{result?result:0}}ms
    <div v-if="result<=250">
      Ninja Fingers
    </div>
    <div v-else-if="result<=400">
      rapid reflexes
    </div>
    <div v-else-if="result>=400">
      Ninja Fingers
    </div>
  </div>

  <div
    v-else-if="result===7000"
    class="score"
  >
    <span>
      game canceled , player click too slow
    </span>

  </div>

  <div v-if="isPlaying">
    <Block
      :isPlaying="isPlaying"
      @end="endGame"
    />
  </div>

</template>

<script>
import Block from "./components/Block.vue";
export default {
  name: "App",
  components: {
    Block,
  },
  data() {
    return {
      isPlaying: false,
      delay: null,
      result: null,
    };
  },
  methods: {
    toggleIsPlaying() {
      this.isPlaying = !this.isPlaying;
      this.result = null;
    },
    endGame(time) {
      this.isPlaying = false;
      this.result = time;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin-top: 60px;
}
button {
  margin: 20px;
  padding: 5px 10px;
}
.score > * {
  margin: 10px;
  font-size: 20px;
  font-weight: bold;
  color: green;
}
.score > span {
  color: red;
}
.info {
  background-color: grey;
  padding: 10px;
  width: 80%;
  margin: 20px auto;
  color: white;
}
</style>
