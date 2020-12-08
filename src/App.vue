<template>
  <div class="container">
    <h1>Reaction Timer</h1>
    <button @click="start" :disabled="playing">play</button>
    <div v-if="playing">
      <Block :delay="delay" @emitTimer="endGame" />
    </div>
    <Results v-if="showResults" :timer="score" />
  </div>
</template>

<script>
import Block from "./components/Block.vue";
import Results from "./components/Results";

export default {
  name: "App",
  components: {
    Block,
    Results,
  },
  data() {
    return {
      playing: false,
      showResults: false,
      delay: null,
      score: null,
    };
  },
  methods: {
    start() {
      this.delay = Math.floor(2000 + Math.random() * 5000);
      this.playing = true;
      this.showResults = false;
    },
    endGame(reactionTime) {
      this.score = reactionTime;
      this.playing = false;
      this.showResults = true;
    },
  },
};
</script>

<style scoped>
body {
  font-family: "Roboto", sans-serif;
}

.container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  text-align: center;
  margin: 0 auto;
}

button {
  width: 200px;
  border-radius: 20px;
  background: #56c7ab;
  color: #fff;
  text-align: center;
  margin: 1rem auto;
}
</style>
