<script setup>
import {ref , computed} from 'vue'
const questions= ref ([
      {
        question: 'Qui est Neo ?',
         answer:0,
        options:[
              'Le hero de matrix',
              'Le nouveau deo a la mode',
              'Le nom de la nouvelle planète decouverte pr^ét de la ceinture dOrion  ',
            ],
            selected: null
        },
        {
        question: 'Ou se trouve Springfield ?',
         answer: 2 ,
        options:[
              'EN dessous du Caire',
              'ça n existe pas ',
              'En Amerique du Nord',
            ],
            selected: null
        },
        {
        question: 'Quelle est la capitale de New York ?',
         answer: 2 ,
        options:[
              'Harlem',
              'Bronkx ',
              'Aucune des deux',
              'New York nest pas une capitale',
            ],
            selected: null
        }
          
          
          ])
        
     
      const quizCompleted = ref(false)
      const currentQuestion = ref(0)
       const score = computed(() => {
       let value = 0
        questions.value.map(q => {
          if(q.selected == q.answer){
            value++
          }
        })
        return value
     })
      const getCurrentQuestion = computed(()=>{
        let question = questions.value[currentQuestion.value]
        question.index = currentQuestion.value
        return question 
      })



     const setAnswer = evt =>{
       questions.value[currentQuestion.value].selected = evt.target.value
       evt.target.value = null
     }
     const nextQuestion = ()=> {
       if (currentQuestion.value < questions.value.lenght -1 ){
         currentQuestion++
       }else{
         quizCompleted.value = true
       }
     }

     
</script>

<template>
<main class="app">
  <h1>QUIZZ</h1>
  <section class="quiz">
    <div class="quiz-info">
      <span class="question">
        {{ getCurrentQuestion.question }}
      </span>
      <span class="score"> Score {{ score }} / {{ questions.lenght }}</span>
    </div>
    <div class="options">
      <label 
      v-for="(option, index) in getCurrentQuestion.options" 
        :key="index"
        :class="` option ${
              getCurrentQuestion.selected == index
              ? index == getCurrentQuestion.answer
              ? 'correct'
              : 'wrong'
              :''
        } ${ 
          getCurrentQuestion.selected != null && 
          index != getCurrentQuestion.selected
          ? 'disabled'
          :''


        }   `"><br>
        <input type="radio" 
        :name=" getCurrentQuestion.index" 
        :value="index"
        v-model="getCurrentQuestion.selected"
        :disabled = "getCurrentQuestion.selected "
        @change="setAnswer">
        <span>{{  option }}</span> <br> <br>

      </label>
    </div>
  </section>

</main>
 
</template>

<style>
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: 'Montserrat', sans-serif;
  }
  body{
    background-color:#271C36;
    color: aqua;
  }
</style>