<template>
    <div class="allCard">
        <displayCard v-for="pokemon in props.pokemons" :key="pokemon.id" @click="handleCardClick(pokemon.id)">
            <template v-slot:title>
                {{ pokemon.name }} # {{ pokemon.id }}
            </template>
            <template v-slot:content>
                <div v-if="pokemon.img">
                    <img :src="pokemon.img" />
                </div>
                <div v-else>
                    <img src="/load.png">
                </div>
            </template>
            <template v-slot:footer>
                <div v-for="feature in pokemon.types" :key="feature.slot">
                    {{ feature.type.name }}
                </div>
            </template>
        </displayCard>
    </div>
</template>

<script setup>
import displayCard from './cardShow.vue';
import {
    defineEmits,
    defineProps,
} from 'vue'
const props = defineProps({
    pokemons: {
        type: [Object],
    },
})

const emit = defineEmits(['buttonClicked'])

const handleCardClick = (id) => {
    emit('buttonClicked', id)
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
