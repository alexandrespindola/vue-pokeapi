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
        poke.value = null
    }
}

getData()

</script>

<template>
    <div v-if="poke" class="flex flex-col items-center justify-center gap-5">
        <img class="w-32 h-auto" :src="poke.sprites?.front_default" alt="">
        <h1 class="text-3xl"><span class="font-bold">Pokemon Name:</span> {{ capitalize(route.params.name) }}</h1>
        <h2 class="text-2xl"><span class="font-bold">ID:</span> {{ poke.id }}</h2>
        <h2 class="text-2xl"><span class="font-bold">Height:</span> {{ poke.height }}</h2>
        <h2 class="text-2xl"><span class="font-bold">Weight:</span> {{ poke.weight }}</h2>
        <div class="flex flex-row items-center gap-5">
            <h2 class="text-2xl"><span class="font-bold">Abilities:</span></h2>
            <ul class="flex flex-row gap-5">
                <li class="text-2xl" v-for="ability in poke.abilities" :key="ability.ability.name">{{ capitalize(ability.ability.name) }}</li>
            </ul>
        </div>
    </div>
    <h1 v-else class="text-4xl">This Pokemon doesn't exist</h1>
    <button class="button text-xl" @click="back">Return</button>
</template>