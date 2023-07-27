<template>
  <header class="bg-white shadow h-16 flex justify-between items-stretch">
    <router-link
      :to="{ name: 'home' }"
      class="inline-flex items-center h-full px-5 text-red-500 font-bold transition-all duration-300 hover:bg-red-500 hover:text-white"
    >
      Home
    </router-link>
    <div class="flex items-center gap-1">
      <router-link
        :to="{ name: 'byName' }"
        class="inline-flex items-center px-2 h-full text-red-500 font-bold transition-all duration-300 hover:bg-red-500 hover:text-white"
      >
        Procure uma refeição
      </router-link>
      <router-link
        :to="{ name: 'byLetter' }"
        class="inline-flex items-center px-2 h-full text-red-500 font-bold transition-all duration-300 hover:bg-red-500 hover:text-white"
      >
        Refeição por letra
      </router-link>
      <router-link
        :to="{ name: 'ingredients' }"
        class="inline-flex items-center px-2 h-full text-red-500 font-bold transition-all duration-300 hover:bg-red-500 hover:text-white"
      >
        Refeição por ingrediente
      </router-link>
    </div>
  </header>
</template>
