<script setup>

import { capitalize } from '../utils/functions.js'
import { RouterLink } from 'vue-router'
import { useGetData } from '@/composables/getData.js'

const { data, getData, loading, error } = useGetData()

getData('https://pokeapi.co/api/v2/pokemon')

</script>

<template>
  <div class="container flex flex-col gap-10">
    <h1 class="text-5xl font-semibold text-center">Pokemons</h1>
    <p class="text-center text-2xl">Click on a Pokemon to see more details</p>
    <p v-if="loading" class="text-center text-xl">Loading information...</p>
    <div v-if="error" class="bg-red-500 text-white p-4 rounded max-w-md mx-auto"> {{ error }}</div>
    <div v-if="data" class="flex flex-col gap-10">
      <div class="flex flex-row justify-center w-75 mx-auto">
        <ul class="flex flex-row justify-center gap-10 flex-wrap ">
          <li v-for="poke in data.results" class="button text-xl">
            <router-link :to="`/pokemons/${poke.name}`"> {{ capitalize(poke.name) }}</router-link>
          </li>
        </ul>
      </div>
      <div class="flex flex-row justify-center gap-5">
        <button @click="getData(data.previous)" 
        :class="{ 'bg-gray-200 text-white pointer-events-none opacity-50': !data.previous }"
          class="bg-green-400 hover:bg-green-500 text-green-700 hover:text-white text-xl font-semibold py-2 px-4 rounded">
          <i class="fas fa-chevron-left mr-2"></i>
          Previous
        </button>
        <button @click="getData(data.next)" 
        :class="{ 'bg-gray-200 text-white pointer-events-none opacity-50': !data.next }"
          class="bg-green-400 hover:bg-green-500 text-green-700 hover:text-white text-xl font-semibold py-2 px-4 rounded">
          Next
          <i class="fas fa-chevron-right ml-2"></i>
        </button>
      </div>
    </div>
  </div>
</template>