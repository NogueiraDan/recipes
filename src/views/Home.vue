<template>
  <div class="p-8 pb-0 text-red-500">
    <h1 class="text-4xl font-bold mb-4">Encontre sua receita</h1>
  </div>

  <!-- LISTAGEM DE RECEITAS ALEATORIAS INICIAIS -->
  <Meals :meals="meals" />
</template>

<script setup>
import { onMounted, ref } from "vue";
import Meals from "../components/Meals.vue";
import axiosClient from "../axiosClient.js";
const meals = ref([]);

onMounted(async () => {
  for (let i = 0; i < 9; i++) {
    const response = await axiosClient.get("/random.php");
    meals.value.push(response.data.meals[0]);
  }
});
</script>
