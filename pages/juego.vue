<template>
    <div id="app">
    <div v-if="pantalla === 'inicio'">
        <h1>¡Piedra, Papel o Tijeras!</h1>
        <button @click="seleccionarJugada('piedra')">Piedra</button>
        <button @click="seleccionarJugada('papel')">Papel</button>
        <button @click="seleccionarJugada('tijeras')">Tijeras</button>
    </div>

    <div v-else-if="pantalla === 'juego'">
        <h2>Tu elección: {{ jugadaJugador }}</h2>
        <h2>Mi elección: {{ jugadaComputadora }}</h2>
        <h3>{{ resultado }}</h3>
        <button @click="reiniciarJuego">Repetir</button>
        <button @click="volverInicio">Volver al Inicio</button>
    </div>
    </div>
</template>

<script>
export default {
    data() {
    return {
        pantalla: 'inicio', // 'inicio' o 'juego'
        jugadaJugador: '',
        jugadaComputadora: '',
        resultado: '',
        opciones: ['piedra', 'papel', 'tijeras'],
    };
    },
    methods: {
    seleccionarJugada(jugada) {
        this.jugadaJugador = jugada;
        this.generarJugadaComputadora();
        this.determinarGanador();
        this.pantalla = 'juego';
    },
    generarJugadaComputadora() {
        const indiceAleatorio = Math.floor(Math.random() * this.opciones.length);
        this.jugadaComputadora = this.opciones[indiceAleatorio];
    },
    determinarGanador() {
        if (this.jugadaJugador === this.jugadaComputadora) {
        this.resultado = '¡Empate!';
        } else if (
        (this.jugadaJugador === 'piedra' && this.jugadaComputadora === 'tijeras') ||
        (this.jugadaJugador === 'papel' && this.jugadaComputadora === 'piedra') ||
        (this.jugadaJugador === 'tijeras' && this.jugadaComputadora === 'papel')
        ) {
        this.resultado = '¡Ganaste!';
        } else {
        this.resultado = '¡Perdiste!';
        }
    },
    reiniciarJuego() {
        this.jugadaJugador = '';
        this.jugadaComputadora = '';
        this.resultado = '';
        this.generarJugadaComputadora();
        this.determinarGanador();
    },
    volverInicio() {
        this.pantalla = 'inicio';
        this.jugadaJugador = '';
        this.jugadaComputadora = '';
        this.resultado = '';
    },
    },
};
</script>