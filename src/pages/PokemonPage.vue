<template>
  <h1 v-if="!pokemon">Please wait...</h1>
  <div v-else>
    <div class="score-container">
      <strong>Score: {{ score }}</strong>
    </div>

    <h1>Who's that pokémon?</h1>

    <PokemonPicture
      class="fade-in"
      :pokemonId="pokemon.id"
      :showPokemon="showPokemon"
    />
    <PokemonOptions
      class="fade-in"
      :pokemons="pokemonArr"
      @selection="checkAnswer"
    />

    <template v-if="showAnswer">
      <h2 class="fade-in">{{ message }}</h2>
      <button class="button" @click="newGame">New Game</button>
    </template>
  </div>
</template>

<script setup lang="ts">
import { ref } from "vue";
import PokemonPicture from "../components/PokemonPicture.vue";
import PokemonOptions from "../components/PokemonOptions.vue";
import getPokemonOptions from "../helpers/getPokemonOptions";
import { Pokemon } from "../models/pokemon";

const pokemonArr = ref<Pokemon[]>([]);
const pokemon = ref<Pokemon>();
const showPokemon = ref(false);
const showAnswer = ref(false);
const message = ref("");
const score = ref(0);

//Methods
const mixPokemonArray = async () => {
  pokemonArr.value = await getPokemonOptions();
  const randomInt = Math.floor(Math.random() * 4);
  pokemon.value = pokemonArr.value[randomInt];
};

const checkAnswer = (pokemonId: number) => {
  if (!pokemon.value) return;

  showPokemon.value = true;
  showAnswer.value = true;

  if (pokemonId === pokemon.value.id) {
    message.value = `CORRECT! Is ${pokemon.value.name}!`;
    score.value += 1;
  } else {
    message.value = `INCORRECT! Is ${pokemon.value.name}!`;
    score.value = 0;
  }
};

const newGame = () => {
  pokemonArr.value = [];
  showPokemon.value = false;
  showAnswer.value = false;
  pokemon.value = undefined;
  mixPokemonArray();
};

mixPokemonArray();
</script>

<style scoped>
.score-container {
  max-width: 90vm;
  display: flex;
  justify-content: flex-end;
  text-align: right;
  font-size: 40px;
  padding-right: 10%;
  /* //margin-left: -200px; */
}
.button {
  background-color: #4caf50; /* Green */
  border: none;
  color: white;
  padding: 15px 32px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  border-radius: 5px;
}
</style>
