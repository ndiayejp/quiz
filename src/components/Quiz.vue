<template>
   <div>
      <h2>{{ quiz.title }}</h2>
      <hr>
      <Progress :value="step" :max="quiz.questions.length - 1"/>
      <Question :key="question.question" :question="question" v-if="state==='question'" @answer="addAnswer"/>
      <Recap v-if="state==='recap'" :quiz="quiz" :answers="answers"/>
      
   </div>
</template>

<script setup>
   import { ref,computed } from "vue"
   import Progress from "../components/Progress.vue"
   import Question from "../components/Question.vue"
   import Recap from "../components/Recap.vue"
   const props =  defineProps({
      quiz : Object
   })
   const step = ref(0)
   const answers = ref(props.quiz.questions.map(()=>null))
   const question = computed(()=>props.quiz.questions[step.value]) 
   const state = ref('question')

   const addAnswer = ((answer)=>{
      answers.value[step.value] = answer
      if(step.value === props.quiz.questions.length - 1){
         state.value = 'recap'
      }else{
         step.value++
      }
   })
</script>