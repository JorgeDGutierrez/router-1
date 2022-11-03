<script setup>
import { RouterLink } from "vue-router";
import { useGetData } from "@/composables/getData";

const { data, getData, loading, error } = useGetData();

getData("https://pokeapi.co/api/v2/pokemon");
</script>

<template>
  <h1>Pokemons</h1>
  <p v-if="loading">Cargando informacion...</p>
  <div class="alert alert-danger mt-2" v-if="error">{{ error }}</div>
  <div v-if="data">
    <ul class="list-group">
      <li class="list-group-item" v-for="poke in data.results">
        <router-link :to="`/pokemons/${poke.name}`">
          {{ poke.name }}
        </router-link>
      </li>
    </ul>
    <div class="mt-2">
      <button
        class="btn btn-outline-danger me-2"
        @click="getData(data.previous)"
        :disabled="data.previous === null"
      >
        Previous
      </button>
      <button
        class="btn btn-outline-primary"
        @click="getData(data.next)"
        :disabled="data.next === null"
      >
        Next
      </button>
    </div>
  </div>
</template>
