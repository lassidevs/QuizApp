<script setup>
    import q from "../data/quizes.json"
    import { ref, watch } from "vue"
    import Card from "../components/Card.vue"

    const quizes = ref(q);
    const search = ref("")
    // watches for any change on the search bar input field
    watch(search, () => {
        // filter quizes based on the current state of the search input. Lowercased because the evaluation is case sensitive!
        quizes.value = q.filter(quiz => quiz.name.toLowerCase().includes(search.value.toLowerCase()))
    })

</script>

<template>
    <header>
      <h1>Quizes</h1>
      <input v-model.trim="search" type="text" placeholder="Search" />
    </header>

    <div class="options-container">
        <Card v-for="quiz in quizes" :key="quiz.id" :quiz="quiz" />
    </div>

</template>

<style scoped>
header {
  margin: 30px 0px 10px 0px;
  display: flex;
  align-items: center;
}

header h1 {
    font-weight: 700;
    margin-right: 30px;
}

header input {
    border: none;
    outline: none;
    background-color: rgba(128, 128, 128, 0.1);
    padding: 10px;
    border-radius: 5px;
}

header input:active,
header input:focus {
    background-color: rgba(128, 128, 128, 0.2);
    transition: .1s ease-in-out;
}


.options-container {
    display: flex;
    flex-wrap: wrap;
    margin-top: 40px
}


</style>