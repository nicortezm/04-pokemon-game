<template>
	<section v-if="isLoading || randomPokemon.id === null"
		class="flex flex-col justify-center items-center w-screen h-screen">
		<h1 class="text-3xl">Espere por favor</h1>
		<h3 class="animate-pulse">Cargando Pokémons</h3>
	</section>

	<section v-else class="flex flex-col justify-center items-center w-screen h-screen">
		<h1 class="m-5">¿Quién es este Pokémon?</h1>
		<!-- <h3 class="capitalize"> {{ gameStatus }}</h3> -->
		<button v-if="gameStatus !== GameStatus.Playing" @click="reset" class=""> Siguiente ronda</button>
		<!-- Pokémon Picture -->

		<PokemonPicture :pokemon-id="randomPokemon.id" :show-pokemon="gameStatus !== GameStatus.Playing" />
		<!-- Pokémon Options -->
		<PokemonOptions :options="options" :block-selection="gameStatus !== GameStatus.Playing"
			@selected-option="checkAnswer" :correct-answer="randomPokemon.id" />
	</section>
</template>

<script setup lang="ts">
import PokemonOptions from '@pokemon/components/PokemonOptions.vue';
import PokemonPicture from '@pokemon/components/PokemonPicture.vue';
import { usePokemonGame } from '@pokemon/composables/usePokemonGame';
import { GameStatus } from '@pokemon/interfaces';

const { randomPokemon, isLoading, gameStatus, getNextOptions, pokemonOptions: options, checkAnswer } = usePokemonGame();

const reset = () => {
	getNextOptions()
}
</script>

<style scoped>
button {
	@apply bg-green-300 shadow-md rounded-lg p-3 m-2 cursor-pointer w-40 text-center transition-all hover:bg-green-100;
}
</style>