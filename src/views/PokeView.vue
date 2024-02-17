<script setup>

import { capitalize } from '../utils/functions.js'
import { useRoute, useRouter } from 'vue-router';
import { useGetData } from '@/composables/getData.js'

const route = useRoute()
const router = useRouter()

const { data, getData, loading, error } = useGetData()

const back = () => {
    router.push('/pokemons')
}

getData(`https://pokeapi.co/api/v2/pokemon/${route.params.name}`)

</script>

<template>
   <p v-if="loading" class="text-center text-xl">Loading information...</p>
   <div v-if="error" class="bg-red-500 text-white p-4 rounded max-w-md mx-auto">{{ error }}</div>
   <div v-if="data" class="flex flex-col items-center justify-center gap-5">
        <img class="w-32 h-auto" :src="data.sprites?.front_default" alt="">
        <h1 class="text-3xl"><span class="font-bold">Pokemon Name:</span> {{ capitalize(route.params.name) }}</h1>
        <h2 class="text-2xl"><span class="font-bold">ID:</span> {{ data.id }}</h2>
        <h2 class="text-2xl"><span class="font-bold">Height:</span> {{ data.height }}</h2>
        <h2 class="text-2xl"><span class="font-bold">Weight:</span> {{ data.weight }}</h2>
        <div class="flex flex-row items-center gap-5">
            <h2 class="text-2xl"><span class="font-bold">Abilities:</span></h2>
            <ul class="flex flex-row gap-5">
                <li class="text-2xl" v-for="ability in data.abilities" :key="ability.ability.name">{{ capitalize(ability.ability.name) }}</li>
            </ul>
        </div>
    </div>
    <h1 v-else class="text-4xl">This Pokemon doesn't exist</h1>
    <button class="button text-xl" @click="back">Return</button>
</template>