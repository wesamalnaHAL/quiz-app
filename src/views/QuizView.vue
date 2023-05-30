<script setup>
    import Questions from "../components/Questions.vue";
    import QuizHeader from "../components/QuizHeader.vue";
    import Result from "../components/Result.vue";
    import { useRoute } from "vue-router";
    import { computed, ref, watch } from "vue";
    import quizes from "../data/quizes.json"

    const route = useRoute()
    const quizId = parseInt(route.params.id)
    const currentQuestionIndex = ref(0)
    const quiz = quizes.find(q => q.id === quizId)
    const numberOfCorrectedAnswers = ref(0)
    const showResults = ref(false)

    const questionStatus = computed(()=> `${currentQuestionIndex.value}/${quiz.questions.length}`)
    const barPerc = computed(()=> `${currentQuestionIndex.value/quiz.questions.length * 100}%   `)

    const onOptionSelected = (isCorrect) => {
        if(isCorrect) {
            numberOfCorrectedAnswers.value++;
        }
        if(quiz.questions.length -1 === currentQuestionIndex.value) {
            showResults.value = true
        }
        currentQuestionIndex.value++;
    }

    // const questionStatus = ref(`${currentQuestionIndex.value}/${quiz.questions.length}`)
    // watch(() => currentQuestionIndex.value, () => {
    //     questionStatus.value = `${currentQuestionIndex.value}/${quiz.questions.length}`
    // })
</script>
<template>
    <div>
        <QuizHeader
            :barPerc="barPerc"
            :questionStatus="questionStatus"/>
        <div>
            <Questions v-if="!showResults" @selectOption="onOptionSelected" :questions="quiz.questions[currentQuestionIndex]" />
            <Result
            :quizQuestionLength="quiz.questions.length"
            :numberOfCorrectedAnswers="numberOfCorrectedAnswers"
            v-else />
        </div>
    </div>
</template>

<style scoped>
  
    
</style>