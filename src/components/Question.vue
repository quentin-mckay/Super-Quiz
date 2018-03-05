<template>
  <div class="wrapper" :class="{ flash: flashActive }">
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
      correctAnswer: 0,
      flashActive: false
    }
  },
  methods: {
    generateQuestion() {
      let nums = []
      for (let i = 0; i < 3; i++) {
        nums.push(this.generateRandomNumber())
      }

      this.num1 = this.generateRandomNumber()
      this.num2 = this.generateRandomNumber()

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
      let correctPosition = this.generateRandomNumber(0, 4);
      console.log(correctPosition)
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
        this.$emit('answered', true)
        this.flashGreen(event.target)
      }
      else {
        this.flashRed(event.target)
      }
    },
    flashRed(el) {

      let keyframes = [
        { backgroundColor: 'red', transform: 'none'},
        { transform: 'translateX(10px)', offset: 0.3 },
        { transform: 'translateX(-10px)', offset: 0.7 },
        { backgroundColor: 'red', transform: 'none'}
      ]

      el.animate(keyframes, 400)
    },
    flashGreen(el) {
      let keyframes = [
        { backgroundColor: 'lightgreen' },
        { backgroundColor: 'initial' },
        
      ]

      el.animate(keyframes, 1000)
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
  width: 40%;
  margin: 0.5rem auto;

  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-row-gap: 1.5rem;
  justify-items: center;

  padding: 1rem;
}

.option {
  padding: 1rem;
  text-align: center;
  background: var(--option-bg);
  color: var(--option-text);
  border-radius: var(--border-radius);
  cursor: pointer;

  transform-origin: center bottom;
}
</style>

