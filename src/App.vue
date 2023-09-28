<template>
  <pokemonCards :pokemons="pokemons" @buttonClicked="pokemonEvolution" />
  <pokemonCards :pokemons="evolution" />
</template>

<script setup>
import { onMounted, ref } from 'vue'
import pokemonCards from './components/pokemonCards.vue'
const pokemonAPI = ref(process.env.VUE_APP_POKEMON_API_URL);


let pokemons = ref('');
let evolution = ref('');
onMounted(() => {
  togetData();
})
const togetData = async () => {
  try {
    let promises = [dataPokemon(1), dataPokemon(4), dataPokemon(7)];
    const returns = await Promise.all(promises);
    pokemons.value = returns.map((data) => ({
      id: data.id,
      name: data.name,
      img: data.img,
      types: data.types,
    }));
  } catch (err) {
    console.error(err);
  }
}

const pokemonEvolution = (id) => {
  let evolutions = [dataPokemon(id + 1), dataPokemon(id + 2)];

  Promise.all(evolutions)
    .then((returned) => {
      evolution.value = returned.map((data) => ({
        id: data.id,
        name: data.name,
        img: data.img,
        types: data.types,
      }));
    })
    .catch((error) => {
      console.error(error);
    });
}


const dataPokemon = async (key) => {
  try {
    const response = await fetch(`${pokemonAPI.value}${key}`);
    const json = await response.json();
    return {
      id: json.id,
      name: json.name,
      img: json.sprites.other["official-artwork"].front_default,
      types: json.types
    };
  } catch (error) {
    console.error(error);
    throw error;
  }
}
</script>

<style scoped></style>
