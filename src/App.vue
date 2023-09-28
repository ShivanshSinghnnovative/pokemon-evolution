<template>
  <div class="allCard">
    <div class="cardContainer"  v-for="pokemon in pokemons" :key="pokemon.id">
      <div class="pokemonCard">
        <div class="pokemonName">
          {{ pokemon.name }} # {{ pokemon.id }}
        </div>
        <hr />
        <div class="pokemonImage">
          <img :src="pokemon.img" />
        </div>
        <hr />
        <div class="pokemonProperty">
          <div v-for="feature in pokemon.types" :key="feature.slot">
            {{ feature.type.name }}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { onMounted, ref } from 'vue'
const pokemonAPI = ref(process.env.VUE_APP_POKEMON_API_URL);

let pokemons = ref('');
onMounted(() => {
  togetData();
})
const togetData = () => {
  let promises = [dataPokemon(1), dataPokemon(4), dataPokemon(7)];
  Promise.all(promises).then((returns) => {
    pokemons.value = returns.map((data) => ({
      id: data.id,
      name: data.name,
      img: data.img,
      types: data.types,
    }));
  })
    .catch(err => console.error(err));

}

async function dataPokemon(key) {
  let response = await fetch(`${pokemonAPI.value}${key}`);
  let json = await response.json();
  return {
    id: json.id,
    name: json.name,
    img: json.sprites.other["official-artwork"].front_default,
    types: json.types
  }
}
</script>

<style scoped>
.allCard {
  display: flex;
  justify-content: space-evenly;
  
}

.cardContainer {
  gap: 2rem;
  margin-top: 5rem;
  cursor: pointer;
}

.pokemonCard {
  border: 1px solid rgb(202, 197, 197);
  box-shadow: 2px 2px 2px 2px lightgray;
  border-radius: .7em;
  width: 20rem;
  height: 28rem;
}

.pokemonName {
  padding: 2rem;
  text-align: center;
  font-size: 30px;
  font-weight: 600;
}

.pokemonImage {
  padding: 2rem;
  text-align: center;
}


img {
  height: 150px;
  width: 150px;
}

.pokemonProperty {
  padding: 1rem;
  text-align: center;
  font-size: 25px;
}
</style>
