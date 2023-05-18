<script setup>
    import {defineProps} from "vue"
    import {RouterLink} from "vue-router"
    const {numberOfCorrectAnswers, quizQuestionLength} = defineProps(['numberOfCorrectAnswers', 'quizQuestionLength'])
</script>

<template>
    <div class="results">
        <p>Your Results...</p>
        <h1>
            {{ numberOfCorrectAnswers }}/{{ quizQuestionLength }}
        </h1>
        <RouterLink to="/">Go Back</RouterLink>
    </div>
</template>

<style scoped>
    a {
        text-decoration: none;
        font-size: 1.2rem;
    }
    .results {
        text-align: center;
        padding: 100px 0px;
    }

    p {
        font-size: 25px;
    }

    h1 {
        font-size: 80px;
    }
</style>