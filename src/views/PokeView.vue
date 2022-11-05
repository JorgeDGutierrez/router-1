<script setup>
import { useRoute, useRouter } from "vue-router";
import { useGetData } from "../composables/getData";
import { useFavoritosStore } from "@/store/favoritos";

const route = useRoute();
const router = useRouter();
const useFavoritos = useFavoritosStore();

const { addFavorito, findPoke } = useFavoritos;

const { data, getData, loading, error } = useGetData();

const back = () => {
  router.push("/pokemons");
};

getData(`https://pokeapi.co/api/v2/pokemon/${route.params.name}`);
</script>

<template>
  <p v-if="loading">Cargando informacion...</p>
  <div class="alert alert-danger mt-2" v-if="error">No existe el pokemon</div>

  <main class="text-center mt-4">

    <div class="card align-content-center">

      <div v-if="data" class="card-header">
        <img :src="data.sprites?.front_default" class="img-fluid img-thumbnail" alt="" />
        <h1 class="card-title">Poke: {{ $route.params.name }}</h1>
        <p class="card-text">Altura: {{ data.height }}</p>
        <p class="card-text">Peso: {{ data.weight }}</p>
        <p class="card-text">Experiencia: {{ data.base_experience }}</p>
        <p>Tipos: {{ data.types?.map((t) => t.type.name).join(", ") }}</p>
        <p class="card-text">Habilidades: {{ data.abilities?.map((a) => a.ability.name).join(", ") }}</p>
        <button :disabled="findPoke(data.name)" class="btn btn-primary me-2" @click="addFavorito(data)">
          Agregar a Favoritos
        </button>
        <button @click="back()" class="btn btn-outline-primary ">Volver al listado</button>
      </div>
    </div>

  </main>
</template>
