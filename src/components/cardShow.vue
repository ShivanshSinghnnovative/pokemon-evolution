<template>
    <div class="cardContainer">
        <div class="pokemonCard">
            <div class="pokemonName">
                <slot name="title"></slot>
            </div>
            <hr />
            <div class="pokemonImage">
                <slot name="content"></slot>
            </div>
            <hr />
            <div class="pokemonProperty">
                <slot name="footer"></slot>
            </div>
        </div>
    </div>
</template>

<script setup>

</script>

<style scoped>
.cardContainer {
    display: flex;
    flex-direction: column;
    gap: 2rem;
    justify-content: center;

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

img {
    height: 50px;
    width: 50px;
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

.pokemonProperty {
    padding: 1rem;
    text-align: center;
    font-size: 25px;
}
</style>
