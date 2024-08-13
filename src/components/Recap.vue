<template>
    <article><b>Score:</b> {{ score }}/{{ props.quiz.questions.length  }}
    <footer> {{ hasWin ? quiz.success_message : quiz.failure_message }}</footer>
    </article>
    
</template>
<script setup>
    import {ref, computed} from "vue"
    const props = defineProps({
        quiz : Object, 
        answers : Array
    })
    const score = computed(()=>{
        return props.quiz.questions.reduce((acc,question,k)=>{
            if(question.correct_answer === props.answers[k]){
                return acc+1;
            }
            return acc; 
        },0)
    })
    const hasWin = computed(()=> score.value >= props.quiz.minimum_score)
</script>