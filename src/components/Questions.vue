<script setup>
import { defineEmits } from 'vue';

const emit = defineEmits(['selectOption'])
defineProps(['questions'])

    const emitSelected = (isCorrect) => {
        emit("selectOption", isCorrect)
    }
 
</script>

<template>
    <div class="question-container">
        <h1 class="question">   
            {{ questions.text }}
        </h1>
    </div>
    <div class="options-container">
        <div v-for="option in questions.options" :key="option.id" @click="emitSelected(option.isCorrect)" class="option">
            <p class="option-label">{{ option.label }} </p>
            <div class="option-value">
                <p>{{ option.text }}</p>
            </div>
        </div>
    </div>
</template>
<style scoped>
.question-container {
    margin-top: 20px;
}
.question {
    font-size: 40px;
    margin-bottom: 20px;
}
.option {
    display: flex;
    cursor: pointer;
}
.option-label {
    background-color: bisque;
    width: 50px;
    height: 50px;
    font-size: 30px;
    display: flex;
    align-items: center;
    justify-content: center;
}
.option-value {
    background-color: rgb(244, 239, 239);
    width: 100%;
    font-size: 20px;
    height: 50px;
    margin-top: 30px;
    padding: 0 20px;
}
</style>