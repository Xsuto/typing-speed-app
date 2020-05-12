<template>
  <div class="Status">
    <h1 class="StatusItem">Words per minute: {{wpm}}</h1>
    <h1 class="StatusItem">Clicks per minute: {{cpm}}</h1>
    <h1 class="StatusItem">You have {{timer}}s left</h1>
  </div>
</template>

<script>
export default {
  name: 'Status',
  props: {
    wpm: Number,
    cpm: Number,
    timer: Number,
  },
};
</script>

<style>
.Status {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  margin: 0;
  padding: 0;
  background-color: #2c3e50;
  color: white;
  width: 100%;
  height: 50vh;
}
.StatusItem {
  display: inline-block;
  font-size: 3rem;
  margin: 0 0 1rem 0;
}
</style>
