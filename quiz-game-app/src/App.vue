<script setup lang="ts">

import ScoreBoard from '@/components/ScoreBoard.vue'
import ResultTotal from './components/ResultTotal.vue';
import { onMounted, reactive, computed, ref } from "vue";
import axios from 'axios';

interface resultsProps {
  questions: string,
  incorrectAnswers: string,
  correctAnswer: string,
  chosenAnswer: undefined,
  answerSubmitedd: boolean,
  winCount: number,
  loseCount: number,
  tryAgain: boolean,
  resultTotal: boolean
}

let results: resultsProps = reactive({
  questions: "",
  incorrectAnswers: "",
  correctAnswer: "",
  chosenAnswer: undefined,
  answerSubmitedd: false,
  winCount: 0,
  loseCount: 0,
  tryAgain: false,
  resultTotal: false
})

const result = ref('')

async function getQuestion() {

  results.questions = ""
  results.chosenAnswer = undefined
  results.answerSubmitedd = false

  await axios.get("https://opentdb.com/api.php?amount=10")
    .then((response) => {
      results.questions = response.data.results[0].question;
      results.incorrectAnswers = response.data.results[0].incorrect_answers;
      results.correctAnswer = response.data.results[0].correct_answer;
    }).catch((error) => {
      console.log(error)
    });
}

onMounted(() => {
  getQuestion()
});

const answer = computed(() => {
  var answer2 = [...results.incorrectAnswers]
  answer2.splice(Number(Math.round(Math.random() * answer2.length)), 0, results.correctAnswer);
  return answer2;
})


async function submitAnswer() {
  if (!results.chosenAnswer) {
    return alert('Select a item for continue!')
  } else {
    const itemSelect = results.chosenAnswer
    const itemCorrect = results.correctAnswer

    results.answerSubmitedd = true;
    if (results.winCount + results.loseCount === 9) {
      results.tryAgain = true
    } else if (results.winCount > results.loseCount) {
      results.resultTotal = true
    }

    if (itemSelect === itemCorrect) {
      results.winCount++
      return result.value = `&#9989 Congratulations. The correct item is: ${itemCorrect}`
    } else {
      results.loseCount++
      return result.value = `&#10060; Error. The correct item is: ${itemCorrect}`
    }
  }


}

</script>

<template>
  <div>
    <template v-if="answer">
      <header>
        <h1>Quiz Game</h1>
      </header>

      <main>
        <ResultTotal v-if="results.tryAgain" :resultTotal="results.resultTotal" />
        <ScoreBoard :winCount="results.winCount" :loseCount="results.loseCount" />
        <section class="question">
          <h1 v-html="results.questions"></h1>
        </section>


        <template v-for="(answers, index) in answer" :key="index">
          <div class="items">
            <input type="radio" name="options" :disabled="results.answerSubmitedd" :value="answers" v-model="results.chosenAnswer">
            <label v-html="answers"></label><br>
          </div>
        </template>
        <section v-if="!results.answerSubmitedd" class="result">
          <button @click="submitAnswer" class="send" type="button">Send</button>
        </section>

        <section v-if="results.answerSubmitedd" class="result">
          <span v-html="result"></span>


          <button @click="getQuestion" class="send" type="button">Next Question</button>
        </section>

      </main>
    </template>
  </div>
</template>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Inter&family=Josefin+Sans&family=Metal+Mania&family=Russo+One&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Inter&family=Josefin+Sans&family=Metal+Mania&display=swap');

header {
  display: flex;
  justify-content: center;
  margin: 30px;
  margin-top: 50px;
  font-family: 'Russo One', Arial, Helvetica, sans-serif;
}

header h1 {
  background-color: blue;
  padding: 10px;
  border-radius: 20px;
  color: #00a8e8;
  font-size: 3rem;
  border: 3px solid black;
  box-shadow: rgba(99, 99, 99, 0.2) 0px 2px 8px 0px;
}

main {
  margin: auto;
  margin-top: 50px;
  min-width: 300px;
  max-width: 1000px;
  padding: 20px;
  font-family: 'Josefin Sans', Arial, Helvetica, sans-serif;
}

.question {
  text-align: center;
  font-size: 1.8rem;
  margin-bottom: 20px;
}

.items {
  width: 100%;
  padding: 15px;
  border-radius: 15px;
  margin: 5px;
  font-size: 1.2rem;
  text-align: center;
  box-shadow: rgba(0, 0, 0, 0.24) 0px 3px 8px;
}

.items input {
  cursor: pointer;
  border: none;
}

.result {
  display: flex;
  flex-direction: column;
  margin-top: 20px;
  font-size: 1.2rem;
  text-align: center;
}

.send {
  margin: 20px auto;
  font-family: 'Josefin Sans', Arial, Helvetica, sans-serif;
  cursor: pointer;
  border-radius: 10px;
  border: none;
  background-color: blue;
  color: #fff;
  text-align: center;
  padding: 5px;
  width: 150px;
  font-size: 1.5rem;
}

.send:hover {
  transition: .3s;
  background-color: #00a8e8;
  border-radius: 20px;
}
</style>
