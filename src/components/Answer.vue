<template>
  <div class="wrapper">
    <p class="message">That's Correct!</p>
    <hr>
    <button @click="clickedNext">Next Question</button>
  </div>
</template>

<script>
export default {
  methods: {
    clickedNext() {
      this.$emit('clickedNext')
    }
  }
}
</script>

<style scoped>
.wrapper {
  margin: 0 auto;
  max-width: var(--panel-width);
  background: var(--answer-bg);
  color: var(--answer-text);
  /* border: 1px solid gray; */
  border-radius: var(--border-radius);

  padding: 1rem;
  text-align: center;
}

.message {
  font-size: 2rem;
  text-align: center;
  font-weight: bold;
}

button {
  background: var(--button-bg);
  color: var(--button-text);
  padding: 1rem 1.5rem;
  border: none;
  border-radius: var(--border-radius);
  font-size: 1rem;
  cursor: pointer;
}


</style>
