<template>
  <div class="wrapper">
    <p class="question">What's {{ num1 }} {{ operator }} {{ num2 }} ?</p>
    <div class="option-grid">
      <div class="option" v-for="(option, index) in options" :key="option.id" @click="guess(index)">
        {{ option }}
      </div>
    </div>
  </div>
</template>

<script>
const MODE_ADDITION = 0
const MODE_SUBTRACTION = 1

export default {
  data() {
    return {
      num1: 0,
      num2: 0,
      operator: '+',
      options: [],
      correctAnswer: 0
    }
  },
  methods: {
    generateQuestion() {
      let nums = []
      for (let i = 0; i < 3; i++) {
        nums.push(this.generateRandomNumber())
      }

      this.num1 = this.generateRandomNumber()
      this.num2 = this.generateRandomNumber(5)

      // create correct answer
      let mode = this.generateRandomNumber(0, 2)
      if (mode === MODE_ADDITION) {
        this.correctAnswer = this.num1 + this.num2
        this.operator = '+'
      }
      else if (mode === MODE_SUBTRACTION) {
        this.correctAnswer = this.num1 - this.num2
        this.operator = '-'
      }

      // put correct answer in random spot
      let correctPosition = this.generateRandomNumber(3);
      nums.splice(correctPosition, 0, this.correctAnswer)

      // set data
      this.options = nums      
    },
    // not including high
    generateRandomNumber(low = -100, high = 100) {
      return Math.floor(Math.random() * (high - low)) + low
    },
    guess(index) {
      if (this.options[index] === this.correctAnswer) {
        console.log('correct')
      }
      else {
        console.log('wrong')
      }
    }
  },
  created() {
    this.generateQuestion()
  }
}
</script>

<style scoped>
.wrapper {
  margin: 1rem auto;
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
  width: 50%;
  margin: 0 auto;

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

