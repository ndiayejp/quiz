<template> 
  <main class="container">
    <div v-if="state==='error'">
      <p>Impossible de charger les données</p>
    </div>
    <div :aria-busy="state==='loading'">
      <Quiz :quiz="quiz" v-if="quiz"/>
    </div>
  </main>
</template>
 
<script setup>
import { onMounted, ref} from 'vue';
import Quiz from "./components/Quiz.vue";
const quiz  = ref(null)
const state = ref('loading')
onMounted(()=>{
  fetch('/quizz.json')
      .then(r=>{
        if(r.ok){
          return r.json();
        }
        throw new Error('impossible de récupérer le json');
      })
      .then((data)=>{
        quiz.value = data
        state.value = "idle"
      })
      .catch((err)=>{
        state.value = "error"
      })
})
</script>