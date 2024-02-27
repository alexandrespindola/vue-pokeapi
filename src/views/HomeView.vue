<script setup>
import { useCounterStore } from '@/store/counter.js'
import { storeToRefs } from 'pinia';

const useCounter = useCounterStore()

const { increment } = useCounter

const { double, count } = storeToRefs(useCounter)

</script>

<template>
  <h1 class="text-5xl font-bold">Vue PokeAPI</h1>
  <RouterLink to="/pokemons" class="button transition-all ease-in-out duration-500 text-2xl">Click to see the Pokemons
    list</RouterLink>
  <h2>Home double counter: {{ double }}</h2>
  <h3>Home counter: {{ count }}</h3>
  <button @click="increment">Increment</button>
</template>
