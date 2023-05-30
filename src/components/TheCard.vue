<template>
    <div class="card" @click="navToQuiz">
        <img :src="quize.img">
        <div class="card-text">
          <h2>{{ quize.name }} </h2>
          <p>{{ quize.questions.length }} question</p>
        </div>
      </div>
</template> 

<script setup>
  import { useRouter } from 'vue-router';
  import { defineProps } from 'vue';
  const {quize} = defineProps(['quize'])

  const router = useRouter()

  const navToQuiz = () => {
    router.push(`/quiz/${quize.id}`)
  }

</script>

<style scoped>
.card {
width: 310px;
overflow: hidden;
border-radius: 2%;
box-shadow: 1px 1px 10px rgba(0, 0, 0, 0.1);
margin-bottom: 35px;
margin-right: 20px;
cursor: pointer;
}
.card img {
width: 100%;
height: 190px;
margin: 0;
}
.card-text {
padding: 0 5px;
}
.card-text h2 {
font-weight: bold;
}
</style>>

