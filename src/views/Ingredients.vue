<template>
  <div class="p-8 pb-0">
    <h1 class="text-4xl font-bold mb-4 text-red-500">Procure ou selecione um ingrediente</h1>
  </div>
  <div class="px-8">
    <input
      type="text"
      v-model="keyword"
      class="rounded border-2 bg-white border-gray-200 focus:ring-red-300 focus:border-red-400 mb-3 w-full"
      placeholder="Search for Ingredients"
    />

    <div class="grid grid-cols-1 md:grid-cols-2 gap-3">
      <div
        v-for="ingredient of computedIngredients"
        :key="ingredient.idIngredient"
      >
        <a
          href="#"
          @click.prevent="openIngredient(ingredient)"
          class="block bg-white rounded p-3 mb-3 shadow text-red-600"
        >
          <h3 class="text-2xl font-bold mb-2">
            {{ ingredient.strIngredient }}
          </h3>
        </a>
      </div>
    </div>
  </div>
</template>

<script setup>
import { computed } from "@vue/reactivity";
import { onMounted, ref } from "vue";
import { useRouter } from "vue-router";
import axiosClient from "../axiosClient";
import store from "../store";

const router = useRouter();
const keyword = ref("");
const ingredients = ref([]);

const computedIngredients = computed(() => {
  if (!computedIngredients) return ingredients;
  const filteredIngredients = ingredients.value.filter((i) =>
    i.strIngredient.toLowerCase().includes(keyword.value.toLowerCase())
  );
  // Ordenando por ordem alfabética
  return filteredIngredients.sort((a, b) =>
    a.strIngredient.localeCompare(b.strIngredient)
  );
});

// Função que leva para as receitas por ingrediente, ao clicar no Ingrediente.
function openIngredient(ingredient) {
  store.commit("setIngredient", ingredient);
  router.push({
    name: "byIngredient",
    params: { ingredient: ingredient.strIngredient },
  });
}

onMounted(() => {
  axiosClient.get("list.php?i=list").then(({ data }) => {
    ingredients.value = data.meals;
  });
});
</script>
