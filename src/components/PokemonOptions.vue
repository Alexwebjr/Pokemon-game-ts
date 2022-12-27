<template>
  <div class="options-container">
    <ul>
      <li
        v-for="pokemon in pokemons"
        :key="pokemon.id"
        @click="$emit('selection', pokemon.id)"
      >
        {{ pokemon.name }}
      </li>
    </ul>
  </div>
</template>

<script setup lang="ts">
import { Pokemon } from "../models/pokemon";

defineProps<{ pokemons: Pokemon[] }>();
</script>

<style>
/* Pokemon Options */
ul {
  list-style-type: none;
}
li {
  background-color: white;
  color: black;
  border-radius: 5px;
  border: 1px solid rgba(0, 0, 0, 0.2);
  cursor: pointer;
  margin-bottom: 10px;
  width: 250px;
}

li:hover {
  background-color: rgba(0, 0, 0, 0.05);
  color: #4caf50;
}

.options-container {
  display: flex;
  justify-content: center;
}
</style>
