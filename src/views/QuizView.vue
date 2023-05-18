<script setup>
    import Question from "../components/Question.vue";
    import QuizHeader from "../components/QuizHeader.vue";
    import Result from "../components/Result.vue"
    import {useRoute} from "vue-router";
    import {ref, watch, computed} from "vue";
    import quizes from "../data/quizes.json"

    const route = useRoute();

    const quizID = parseInt(route.params.id);
    const quiz = quizes.find(q => q.id === quizID)
    // Keep state of the question the client is on
    const currentQuestionIndex = ref(0)

    const numberOfCorrectAnswers = ref(0);
    const showResults = ref(false)

    // Watch for changes in values inside the computed function. If changes occur, recompute the questionStatus
    const questionStatus = computed(() => `${currentQuestionIndex.value}/${quiz.questions.length}`)
    const barPercentage = computed(() => `${currentQuestionIndex.value/quiz.questions.length * 100}%`)

    const handleOptionSelection = (isCorrect) => {
        if(isCorrect) {
            numberOfCorrectAnswers.value++
        } 
        if(currentQuestionIndex.value === quiz.questions.length - 1 ) {
            currentQuestionIndex.value++
            return showResults.value = true;
        } else {
            currentQuestionIndex.value++
        }
    }

</script>



<template>
    <div>
        <QuizHeader 
            :questionStatus="questionStatus"
            :barPercentage="barPercentage"
        />
        <div >
            <Question 
                v-if="!showResults"
                :question="quiz.questions[currentQuestionIndex]" 
                @optionSelected="handleOptionSelection"
            />
            <Result 
                v-else
                :numberOfCorrectAnswers="numberOfCorrectAnswers" 
                :quizQuestionLength="quiz.questions.length"
            />
        </div>
    </div>
</template>

