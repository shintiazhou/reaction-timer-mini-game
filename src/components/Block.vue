<template>
  <div
    class="container"
    @click="endTimer"
    v-if="startGame"
  >
    <div>
      click me
      quick!!!!
    </div>

    <div>{{prompt}}</div>
  </div>
</template>

<script>
export default {
  name: "Block",
  props: {
    isPlaying: Boolean,
  },
  data() {
    return {
      delay: null,
      timer: null,
      reactionTime: 0,
      startGame: false,
      prompt: "",
    };
  },
  methods: {
    startTimer() {
      this.timer = setInterval(() => {
        this.reactionTime += 10;
        if (this.reactionTime >= 5000) {
          this.prompt = "u gonna click or no";
        }
        if (this.reactionTime >= 7000) {
          this.endTimer();
        }
      }, 10);
    },
    endTimer() {
      clearInterval(this.timer);
      this.startGame = false;
      this.$emit("end", this.reactionTime);
    },
  },
  mounted() {
    if (this.isPlaying === true) {
      this.delay = 2000 + Math.random() * 5000;
    }
    setTimeout(() => {
      this.startGame = true;
      this.startTimer();
    }, this.delay);
  },
};
</script>

<style>
.container {
  background-color: burlywood;
  width: 400px;
  height: 350px;
  margin: 30px auto;
  display: flex;
  justify-content: center;
  align-items: center;
  font-weight: bold;
  cursor: pointer;
}
</style>