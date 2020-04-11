/* eslint-disable no-undef */
<template>
    <div class="question-box-container">
        <b-jumbotron>
            
            <template v-slot:lead>
            {{currentQuestion.question}}
            </template>

            <hr class="my-4">
            <b-list-group>
                <b-list-group-item v-for="(answer, index) in answers" :key="index"
                @click.prevent = "selectAnswer(index)"
                :class="[selectedIndex === index ? 'selected' : '']"
                >
                {{answer}}</b-list-group-item>
            </b-list-group>
                  
            <b-button variant="primary" href="#">Submit</b-button>
            <b-button @click="next" variant="success" href="#">Next</b-button>
        </b-jumbotron>
    </div>
</template>

<script>
    //whevever you a passing a data or methods, we need to pass the question here as a prop to use it in this component
    export default {
        props: {
            currentQuestion: Object,
            next: Function
        },
        //saving the index selected in the methods function below
        data(){
            return{
                selectedIndex: null
            }
        },
    computed: {
        answers() {
            //the 3 dots basically means making a copy of the array instead of referencing thesame array
            //if you want to access another method or prop in javascript, you need to  use the this keyword
            let answers = [...this.currentQuestion.incorrect_answers]
            answers.push(this.currentQuestion.correct_answer)
            return answers
        }
      },
      methods: {
          //basically logging the index of the answers array to the console
            selectAnswer(index){
                this.selectedIndex = index
            }
      },

      mounted(){
          console.log(this.currentQuestion)
      }
    }
</script>

<style scoped>
    .list-group{
        margin-bottom: 15px;
    }

     .list-group-item:hover{
        background: #eee;
        cursor: pointer;
    }

    .btn{
        margin: 0 5px;
    }

    .selected{
        background-color: lightblue;
    }

    .correct{
        background-color: lightgreen;
    }

    .incorrect{
        background-color:red;
    }
</style>