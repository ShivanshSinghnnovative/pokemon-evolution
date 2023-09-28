<template>
  <div class="allCard">
    <cardShow v-for="pokemon in pokemons" :key="pokemon.id" @click="handleCardClick(pokemon.id)">
      <template v-slot:title>
        {{ pokemon.name }} # {{ pokemon.id }}
      </template>
      <template v-slot:content>
        <img :src="pokemon.img" />
      </template>
      <template v-slot:footer>
        <div v-for="feature in pokemon.types" :key="feature.slot">
          {{ feature.type.name }}
        </div>
      </template>
    </cardShow>
  </div>
</template>

<script setup>
import { onMounted, ref } from 'vue'
import cardShow from './components/cardShow.vue'
const pokemonAPI = ref(process.env.VUE_APP_POKEMON_API_URL);

let pokemons = ref('');
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

<style scoped>
.allCard {
  display: flex;
  justify-content: space-evenly;

}

img {
  height: 150px;
  width: 150px;
}
</style>
