<template>
  <div id="app">
    <status :cpm="cpm" :wpm="wpm" :timer="timer" />
    <text-place-holder @updateTimer="updateTimer" @updateCpm="updateCpm" @updateWpm="updateWpm" />
    <restart-button v-show="!timer" @restart="handleRestart" />
  </div>
</template>

<script>
import Status from './components/Status.vue';
import TextPlaceHolder from './components/TextPlaceholder.vue';
import RestartButton from './components/RestartButton.vue';

export default {
  name: 'App',
  components: {
    Status,
    TextPlaceHolder,
    RestartButton,
  },
  data() {
    return {
      cpm: 0,
      wpm: 0,
      timer: 60,
    };
  },
  methods: {
    updateTimer(timer) {
      this.timer = timer;
    },
    updateCpm(cpm) {
      this.cpm += cpm;
    },
    updateWpm(wpm) {
      this.wpm += wpm;
    },
    handleRestart() {
      this.wpm -= this.wpm;
      this.cpm -= this.cpm;
      this.$emit('restartTextPlaceHolder');
    },
  },
};
</script>

<style>
html,
body {
  margin: 0;
  padding: 0;
}
#app {
  padding: 0;
  margin: 0;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  min-height: 100vh;
  min-width: 100vw;
}
</style>
