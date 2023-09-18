<template>
    <h1 v-if="isLoading">Buscando...</h1>
    <h1 v-else-if="errorMessage">{{ errorMessage }}</h1>

    <template v-else>
        <h3>{{ pokemon.name }}</h3>
        <img :src="pokemon.sprites.front_default" :alt="pokemon.name">
        <br>
        <router-link :to="{ name: 'pokemon-search' }">Regresar</router-link>
    </template>
</template>

<script>
import { watch } from 'vue';
import { useRoute, onBeforeRouteLeave } from 'vue-router';
import usePokemon from '../composables/usePokemon'

export default {
    setup() {
        const route = useRoute()
        const { pokemon, isLoading, errorMessage, searchPokemon } = usePokemon(route.params.id)

        // Watch
        watch(
            () => route.params.id, // Observa
            () => searchPokemon(route.params.id) // Lanza cuando cambia observado
        )

        onBeforeRouteLeave(() => {
            const answer = window.confirm('¿Estás seguro que deseas salir?')

            if (!answer) return false // Bloquea la salida
        })

        return {
            errorMessage,
            isLoading,
            pokemon,
        }
    }
}
</script>

<style lang="scss" scoped></style>