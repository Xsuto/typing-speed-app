<template>
  <div class="TextPlaceholder">
    <div class="done">
      <p class="doneText" v-bind:class="{ space: needSpace }">{{ doneWords }}</p>
    </div>
    <div class="working">
      <div class="Text" v-for="word in firstTenWords" :key="word">{{ word }}</div>
    </div>
  </div>
</template>

<script>
import randomWords from 'random-words';

export default {
  data() {
    return {
      words: randomWords(200),
      doneWords: '',
      timer: 60,
      timerId: null,
      started: false,
      needSpace: false,
    };
  },
  computed: {
    firstTenWords() {
      return this.words.slice(0, 10);
    },
  },
  watch: {
    timer() {
      this.$emit('updateTimer', this.timer);
      if (this.timer <= 0) clearInterval(this.timerId);
    },
    doneWords() {
      if (this.doneWords.length > 25) {
        this.doneWords = this.doneWords.substring(1);
      }
    },
  },
  methods: {
    handleClick(e) {
      if (this.timer > 0) {
        if (!this.firstTenWords[0].length && e.keyCode === 32) {
          this.needSpace = true;
          this.doneWords += ' ';
          this.$emit('updateWpm', 1);
          this.$emit('updateCpm', 1);
          this.words.shift();
        }
        if (e.key !== this.firstTenWords[0].charAt(0)) return;
        if (!this.started) this.startTimer();
        this.needSpace = false;
        this.doneWords += e.key;
        this.$emit('updateCpm', 1);
        this.firstTenWords[0] = this.firstTenWords[0].substring(1);
      }
    },
    startTimer() {
      this.started = true;
      this.timerId = setInterval(() => {
        this.timer -= 1;
      }, 1000);
    },
    restart() {
      try {
        clearInterval(this.timerId);
        this.timer = 60;
        this.timerId = null;
      } catch {
        this.timer = 60;
        this.timerId = null;
      }
      this.words = randomWords(200);
      this.doneWords = '';

      this.started = false;
      this.needSpace = false;
    },
  },
  created() {
    window.addEventListener('keydown', (e) => this.handleClick(e));
    this.$parent.$on('restartTextPlaceHolder', this.restart);
  },
};
</script>

<style>
.TextPlaceholder {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 10vh;
  background-color: rgb(224, 217, 217);

  width: 100%;
  font-size: 1rem;
}
.done,
.working {
  width: 50%;
  font-size: 2rem;
}
.working {
  padding: 0;
  border-left: 2px solid blue;
  animation: borderBlink 1s step-end infinite;
  text-align: start;
}

.doneText {
  text-align: end;
  color: rgb(76, 135, 150);
}
.Text {
  display: inline;
  margin: 0 1rem 0 0;
}
.space {
  padding: 0 1rem 0 0;
}
@keyframes borderBlink {
  from,
  to {
    border-color: transparent;
  }
  50% {
    border-color: blue;
  }
}
</style>
