<template>
  <div class="pokemon-container">
    <img
      v-if="!showPokemon"
      :src="imgSrc"
      alt="pokemon"
      class="hidden-pokemon"
    />
    <img v-else :src="imgSrc" alt="pokemon" class="fade-in" />
  </div>
</template>

<script setup lang="ts">
import { computed } from "vue";

const props = defineProps<{
  pokemonId: number;
  showPokemon: boolean;
}>();

const imgSrc = computed(
  () =>
    `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/${props.pokemonId}.svg`
);
</script>

<style scoped>
/* Pokemon Picture */
.pokemon-container {
  height: 200px;
  display: flex;
  justify-content: center;
}
img {
  height: 200px;
  position: absolute;
  /*   right: 32%;
  width: 100vw;
  margin-left: -50vw; */
  user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  -webkit-user-drag: none;
  -webkit-user-select: none;
}
.hidden-pokemon {
  filter: brightness(0);
}
</style>
