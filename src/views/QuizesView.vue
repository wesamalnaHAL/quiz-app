<template>
<div>
<header>
  <h1>Quizes</h1>
  <input v-model.trim="search" type="text" placeholder="Search...">
</header>
<div class="options-container">
  <TheCard v-for="quize in quizes" :key="quize.id" :quize="quize"/>
</div>
</div>
</template>

<script setup>
import q from "../data/quizes.json"
import {ref, watch} from 'vue';
import TheCard from "../components/TheCard.vue";

const quizes = ref(q)
const search = ref("")

watch(search, () => {
quizes.value = q.filter(quize => quize.name.toLowerCase().includes(search.value.toLocaleLowerCase()))
})




</script>

<style scoped>


header {
margin-bottom: 10px;
margin-top: 30px;
display: flex;
align-items: center;
}
header h1 {
font-weight: bold;
margin-right: 30px;
}
header input {
border: none;
background-color: rgba(128, 128, 128, 0.1);
padding: 10px;
border-radius: 5px;
}
.options-container {
display: flex;
flex-wrap: wrap;
margin-top: 40px;
}

</style>