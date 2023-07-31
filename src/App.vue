<script setup>
import { ref, reactive } from "vue";
import Questions from "./components/Questions.vue";
import Results from "./components/Results.vue";

let questionsAnswered = ref(0);
let totalCorrect = ref(0);

let questions = reactive([
  {
    q: "What is the Composition API in Vue.js 3?",
    answers: [
      {
        option: "A) A new way of writing HTML templates",
        correctAns: false,
      },
      {
        option: "B) A powerful tool for organizing Vuex store mutations",
        correctAns: false,
      },
      {
        option:
          "C) A feature that allows you to use React components within a Vue.js app",
        correctAns: false,
      },
      {
        option: "D) An alternative way to organize and reuse component logic",
        correctAns: true,
      },
    ],
  },
  {
    q: "Which of the following is a new feature introduced in Vue.js 3?",
    answers: [
      {
        option: "A) The v-bind directive for data binding",
        correctAns: false,
      },
      {
        option: "B) The Options API for defining Vue components",
        correctAns: false,
      },
      {
        option: "C) The Composition API for organizing component logic",
        correctAns: true,
      },
      {
        option:
          "D) The v-for directive for looping through arrays in templates",
        correctAns: false,
      },
    ],
  },
  {
    q: "What is the purpose of the setup function in the Composition API of Vue.js 3?",
    answers: [
      {
        option: "A) A new way of writing HTML templates",
        correctAns: false,
      },
      {
        option: "B) A powerful tool for organizing Vuex store mutations",
        correctAns: false,
      },
      {
        option:
          " C) feature that allows you to use React components within a Vue.js app",
        correctAns: false,
      },
      {
        option:
          "D) It is the entry point for defining component logic and data.",
        correctAns: true,
      },
    ],
  },
]);

let results = reactive([
  {
    min: 0,
    max: 2,
    title: "Try again!",
    desc: "Do a little more studying and you may succeed!",
  },
  {
    min: 3,
    max: 3,
    title: "Wow, you're a genius!",
    desc: "Studying has definitely paid off for you!",
  },
]);

let questionAnswered = (isCorrect) => {
  if (isCorrect) {
    totalCorrect.value++;
  }
  questionsAnswered.value++;
};

let reset = () => {
  questionsAnswered.value = 0;
  totalCorrect.value = 0;
};
</script>


<template>
  <div class="ctr">
    <transition name="fade" mode="out-in">
      <Questions
        v-if="questionsAnswered < questions.length"
        :questions="questions"
        :questionsAnswered="questionsAnswered"
        @question-answered="questionAnswered"
      />
      <Results v-else :results="results" :totalCorrect="totalCorrect"/>
    </transition>

    <button
      type="button"
      class="reset-btn"
      @click.prevent="reset"
      v-if="questionsAnswered === questions.length"
    >
      Reset
    </button>
  </div>
</template>


<style scoped>
</style>