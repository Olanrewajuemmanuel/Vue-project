<template>
  <div class="">
    <b-jumbotron header="Questions" lead="choose an option">
      <div class="my-4">
        <p>{{ currQuestion.question }}</p>
        <div class="options m-3">
          <b-list-group v-for="(answer, index) in answers" :key="index">
            <b-list-group-item
              class="mt-3 mb-2"
              :class="[selectedIndex == index ? 'selected' : '']"
              @click="selectAnswer(index)"
              >{{ answer }}</b-list-group-item
            >
          </b-list-group>
        </div>
        <b-button variant="success mr-3" @click="submitAnswer" :disabled="selectedIndex === null">Submit</b-button>
        <b-button @click="next" variant="primary">Next</b-button>
      </div>
    </b-jumbotron>
  </div>
</template>

<script>
import _ from "lodash";
// In order for the props to be displayed in HTML
export default {
  props: {
    currQuestion: Object,
    next: Function,
    increment: Function
  },
  computed: {
    answers() {
      let answers = [
        ...this.currQuestion.incorrect_answers,
      ];

      answers.push(this.currQuestion.correct_answer);
      return answers;
    },
  },
  data() {
    return {
      selectedIndex: null,
      shuffledAnswers: [],
    };
  },
  methods: {
    selectAnswer(index) {
      this.selectedIndex = index;
    },
    shuffleAnswers() {
      let answers = [
        ...this.currQuestion.incorrect_answers,
        this.currentQuestion.correct_answer,
      ];
      // Use lodash to shuffle
      this.shuffledAnswers = _.shuffle(answers);
    },
    submitAnswer() {
        let isCorrect = false
        if (this.selectedIndex === this.correctIndex) {
            isCorrect = true
        }
        this.increment(isCorrect)
    },
  },
  watch: {
    currentQuestion() {
      this.selectedIndex = null;
      this.shuffleAnswers();
    },
  },
};
</script>

<style scoped>
.list-group-item:hover {
  background-color: #f1f1f1;
  cursor: pointer;
}
.selected {
  background-color: rgb(0, 119, 255) !important;
}
.correct {
  background-color: lightgreen;
}
.incorrect {
  background-color: red;
}
</style>