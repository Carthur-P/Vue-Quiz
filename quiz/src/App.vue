<template>
  <div id="app">
    <Header />
    <QuestionBox :question="quizData[currentQuestion]" :next="next" v-if="quizData.length != 0"/>
  </div>
</template>

<script>
import Header from "./components/Header";
import QuestionBox from "./components/QuestionBox";

export default {
  name: "App",
  components: {
    Header,
    QuestionBox,
  },
  data(){
    return {
      quizData: [],
      currentQuestion: 0
    }
  },
  methods: {
    next(){
      if(this.currentQuestion < this.quizData.length - 1){
        this.currentQuestion ++; 
        console.log(this.currentQuestion);
      }
    }
  },
  mounted() {
    fetch("https://opentdb.com/api.php?amount=10&type=multiple")
    .then((res) => res.json())
    .then((data) => {
      this.quizData = data.results;
    })
    .catch(err => {
      console.log(err);
    });
  }
};
</script>

<style>
* {
  padding: 0px;
  margin: 0px;
}
</style>
