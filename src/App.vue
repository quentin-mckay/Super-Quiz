<template>
  <div class="container">
    <h1>The Super Quiz</h1>
    <hr>
    <component :is="selectedComponent" @answered="answered" @clickedNext="clickedNext"></component>
  </div>
</template>

<script>
import Question from './components/Question.vue'
import Answer from './components/Answer.vue'


export default {
  components: {
    appQuestion: Question,
    appAnswer: Answer
  },
  data() {
    return {
      selectedComponent: 'app-question',
      answer: ''
    }
  },
  methods: {
    answered(isAnswerCorrect) {
      if (isAnswerCorrect === false) {
        alert('Wrong. Try again!')
      }
      else {
        this.selectedComponent = 'app-answer'
      }
    },
    clickedNext() {
      this.selectedComponent = 'app-question'
    }
  }

}
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Roboto');

:root {
  --bg: #eee;
  --font: black;
  --panel-width: 500px;
  --option-text: white;
  --option-bg: steelblue;
  --answer-bg: rgb(208, 224, 208);
  --answer-text: rgb(47, 109, 47);
  --button-bg: steelblue;
  --button-text: white;

  --border-radius: 5px;
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  background: var(--bg);
  font-family: Roboto;
  color: var(--font);
}

h1 {
  text-align: center;
  font-size: 3rem;
}

hr {
  border-bottom: 1px solid rgba(128, 128, 128, 0.2);
  margin: 1rem 0;
}

.container {
  max-width: 600px;
  margin: 3rem auto;
}


</style>
