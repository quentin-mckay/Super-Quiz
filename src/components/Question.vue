<template>
  <div class="wrapper">
    <p class="question">What's {{ num1 }} {{ operator }} {{ num2 }}</p>
    <div class="option-grid">
      <div class="option" v-for="option in options" :key="option.id">
        {{ option }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      num1: 0,
      num2: 0,
      operator: '+',
      options: [1, 2, 3, 4]
    }
  },
  methods: {
    generateQuestion() {
      
    }
  },
  created() {
    this.generateQuestion()
  }
}
</script>

<style scoped>
.wrapper {
  margin: 0 auto;
  max-width: var(--panel-width);
  border: 1px solid gray;
  border-radius: var(--border-radius);

  overflow: hidden;
}

.question {
  text-align: center;
  font-size: 1.2rem;
  background: lightgray;
  padding: 0.5rem 0;
  font-weight: bold;
}

.option-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-gap: 1rem;
  justify-items: center;

  padding: 1rem;
}

.option {
  padding: 1rem;
  text-align: center;
  background: var(--option-bg);
  color: var(--option-text);
  border-radius: var(--border-radius);
}
</style>
