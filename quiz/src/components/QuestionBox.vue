<template>
  <div class="container">
    <p>{{ question.question }}</p>
    <p
      class="answer"
      :key="index"
      v-for="(answer, index) in answers"
      @click="answerSelect(index)"
      :class="[selectedIndex === index ? 'selected' : '']"
    >
      {{ answer }}
    </p>
    <div class="buttonContainer">
      <button>Submit</button>
      <button @click="next">Next</button>
    </div>
  </div>
</template>

<script>
import shuffle from "shuffle-array";

export default {
  name: "QuestionBox",
  props: ["question", "next"],
  data() {
    return {
      selectedIndex: null,
    };
  },
  computed: {
    answers() {
      let options = this.question.incorrect_answers;
      options.push(this.question.correct_answer);
      return shuffle(options);
    },
  },
  methods: {
    answerSelect(index) {
      this.selectedIndex = index;
      console.log(this.selectedIndex);
    },
  },
};
</script>

<style scoped>
p:first-child {
  margin-bottom: 10px;
}

.container {
  margin: auto;
  padding: 20px;
  border-radius: 10px;
  background-color: beige;
  width: 80vw;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.buttonContainer {
  margin-top: 10px;
}

.answer {
  background-color: whitesmoke;
  margin: 10px 0px;
  padding: 20px;
  min-width: 200px;
  text-align: center;
  border-radius: 10px;
  border: 2px solid thistle;
}

.answer:hover {
  background-color: lightgrey;
}

.selected {
  background-color: darkgray;
}
</style>
