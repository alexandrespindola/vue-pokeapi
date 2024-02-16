<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <header>
    <div class="flex bg-green-600">
      <nav class="container mx-auto flex items-center justify-between flex-wrap p-6">
        <RouterLink to="/">
          <div class="flex items-center flex-shrink-0 text-white mr-6 gap-4">
            <i class="fab fa-vuejs text-2xl"></i>
            <span class="font-semibold text-xl tracking-tight">Vue PokeAPI</span>
          </div>
        </RouterLink>
        <div class="flex flex-row gap-5">
          <RouterLink to="/pokemons" class="button transition-all ease-in-out duration-500 flex flex-row items-center gap-3">Pokemons</RouterLink>
          <a href="https://github.com/alexandrespindola/vue-pokeapi" target="_blank" >
            <button class="button transition-all ease-in-out duration-500 flex flex-row items-center gap-3">
              <i class="fab fa-github text-2xl"></i>
              Code
            </button>
          </a>
        </div>
      </nav>
    </div>
  </header>

  <main class="bg-grey-300 flex flex-col items-center justify-center p-10">
    <div class="main__div container main__div bg-green-200 flex flex-col items-center justify-center h-full rounded-xl gap-10 ">
      <RouterView />
    </div>
  </main>
</template>
<style scoped></style>
