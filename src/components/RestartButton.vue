<template>
  <button class="RestartBtn" @click="handleClick">Restart</button>
</template>

<script>
export default {
  methods: {
    handleClick() {
      this.$emit('restart');
    },
  },
};
</script>

<style>
.RestartBtn {
  margin: 3rem 0 0 0;
  width: 30rem;
  height: 4.5rem;
  font-size: 3rem;
  background: none;
  border: none;
  background-color: rgba(50, 50, 200, 0.2);
  border: 2px solid #2c3e50;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  color: #2c3e50;
}
</style>
