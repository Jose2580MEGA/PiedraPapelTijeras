<template>
    <div class="container">
    <h1>¡Piedra, Papel o Tijeras!</h1>

    <div v-if="!jugadaJugador">
        <p>Elige tu jugada:</p>
        <button @click="seleccionarJugada('piedra')">Piedra</button>
        <button @click="seleccionarJugada('papel')">Papel</button>
        <button @click="seleccionarJugada('tijeras')">Tijeras</button>
    </div>

    <div v-else class="resultado-container">
        <h2>Tu elección: {{ jugadaJugador }}</h2>
        <h2>Mi elección: {{ jugadaComputadora }}</h2>
        <h3>{{ resultado }}</h3>
        <button @click="reiniciarJuego">Repetir</button>
        <button>
        <NuxtLink to="/">Volver al Inicio</NuxtLink>
        </button>
    </div>
    </div>
</template>

<script setup>
import { ref } from 'vue';

const jugadaJugador = ref('');
const jugadaComputadora = ref('');
const resultado = ref('');
const opciones = ['piedra', 'papel', 'tijeras'];

const generarJugadaComputadora = () => {
    const indiceAleatorio = Math.floor(Math.random() * opciones.length);
    jugadaComputadora.value = opciones[indiceAleatorio];
};

const determinarGanador = () => {
    if (jugadaJugador.value === jugadaComputadora.value) {
        resultado.value = '¡Empate!';
    } else if (
        (jugadaJugador.value === 'piedra' && jugadaComputadora.value === 'tijeras') ||
        (jugadaJugador.value === 'papel' && jugadaComputadora.value === 'piedra') ||
        (jugadaJugador.value === 'tijeras' && jugadaComputadora.value === 'papel')
    ) {
        resultado.value = '¡Ganaste!';
    } else {
        resultado.value = '¡Perdiste!';
    }
};

const seleccionarJugada = (jugada) => {
    jugadaJugador.value = jugada;
    generarJugadaComputadora();
    determinarGanador();
};

const reiniciarJuego = () => {
    jugadaJugador.value = '';
    jugadaComputadora.value = '';
    resultado.value = '';
};
</script>