<template>
    <div class="question">
        <h4>{{ question.question }}</h4>
        <ul>
            <li v-for="(choice,index) in question.choices " :key="choice">
                <label for="`answer{{index }}`">
                    <input id="`answer{{index }}`" type="radio" name="answer" v-model="answer" :value="choice"> {{ choice }}
                </label>
            </li>
        </ul>
        <div class="button">
            <button :disabled="!hasAnswer" @click="emit('answer',answer)">Question suivante</button>
        </div>
    </div> 
</template>
<script setup>
    import {ref,computed} from "vue"
    const props = defineProps({
        question : Object
    })
    const answer = ref(null)
    const emit = defineEmits(['answer'])
    const hasAnswer = computed(()=> answer.value !==null)
</script>

<style>
    .question .button{
        display: flex;
        justify-content: end;
    }
    .question ul li{
        list-style: none;
        padding: 0 ;
    }
    .question ul{ padding: 0;}

</style>