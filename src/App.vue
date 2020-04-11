<template>
  <div id="app">
    <Header/>
      <b-container class="bv-example-row">
          <b-row>
            <b-col sm="6" offset="3">
              <QuestionBox
              v-if="questions.length"
              :currentQuestion="questions[index]"
              :next="next"
              />
            </b-col>
          </b-row>
      </b-container>   
  </div>
</template>

<script>
import Header from './components/Header.vue'
import QuestionBox from './components/QuestionBox.vue'

export default {
  name: 'App',
  components: {
    Header,
    QuestionBox
  },

  data() {
    return{
      questions: [],
      //pass the start of the question
      index: 0

    }
  },
  methods: {
    next: function(){
      this.index++
    }
  },

  mounted: function(){
    fetch('https://opentdb.com/api.php?amount=10&category=27&type=multiple',
    {
      method: 'get'
    })
    //get the response from the api
    .then((response)=>{
      return response.json()
    })
    //this is where we want to access data from the application
    .then((jsonData)=>{
      //getting the questions from the api which is under the results array
      this.questions = jsonData.results
    })
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
