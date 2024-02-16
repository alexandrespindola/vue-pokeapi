<script setup>

import { ref } from 'vue'
import { capitalize } from '../utils/functions.js'
import axios from 'axios';
import { useRoute, useRouter } from 'vue-router';

const route = useRoute()
const router = useRouter()

const back = () => {
    router.push('/pokemons')
}

const poke = ref({})

const getData = async () => {
    try {
        const { data } = await axios.get(`https://pokeapi.co/api/v2/pokemon/${route.params.name}`)
        console.log(data)
        poke.value = data
    } catch (error) {
        console.error(error)
    }
}

getData()

</script>

<template>
    <img :src="poke.sprites?.front_default" alt="">
    <h1>Pokemon name: {{ capitalize(route.params.name) }}</h1>
    <button @click="back">Return</button>
</template>