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
    <h1>Pokemons</h1>
    <ul>
      <li v-for="poke in pokemons">
        <router-link :to="`/pokemons/${poke.name}`"> {{ capitalize(poke.name) }}</router-link>
      </li>
    </ul>
</template>