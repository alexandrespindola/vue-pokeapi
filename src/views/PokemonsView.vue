<script setup>

import axios from 'axios'
import { ref } from 'vue'
import { capitalize } from '../utils/functions.js'
import { RouterLink } from 'vue-router'

const pokemons = ref([])

const getData = async () => {
  try {
    const response = await axios.get('https://pokeapi.co/api/v2/pokemon')
    pokemons.value = response.data.results
  } catch (error) {
    console.error(error)
  }
}

getData()

</script>

<template>
    <div class="container flex flex-col gap-10">
    <h1 class="text-5xl font-semibold text-center">Pokemons</h1>
    <p class="text-center">Click on a Pokemon to see more details</p>
      <div class="flex flex-row justify-center w-75 mx-auto">
        <ul class="flex flex-row justify-center gap-10 flex-wrap ">
          <li v-for="poke in pokemons" class="button">
            <router-link :to="`/pokemons/${poke.name}`"> {{ capitalize(poke.name) }}</router-link>
          </li>
        </ul>
      </div>
    </div>
</template>