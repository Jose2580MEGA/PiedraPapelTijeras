<template>
  <div class="container">
    <div v-if="gameState === 'initial'" class="initial-screen">
      <h1>Piedra, Papel o Tijeras</h1>
      <button @click="startGame" class="play-button">Jugar</button>
    </div>

    <div v-if="gameState === 'selection'" class="selection-screen">
      <h2>Elige tu jugada:</h2>
      <div class="choices">
        <button @click="play('piedra')" class="choice-button">Piedra</button>
        <button @click="play('papel')" class="choice-button">Papel</button>
        <button @click="play('tijeras')" class="choice-button">Tijeras</button>
      </div>
    </div>

    <div v-if="gameState === 'result'" class="result-screen">
      <h2>Resultado:</h2>
      <p>Tu jugada: {{ playerChoice }}</p>
      <p>Jugada de la máquina: {{ computerChoice }}</p>
      <h3 v-if="result === 'ganaste'">¡Ganaste! 🎉</h3>
      <h3 v-else-if="result === 'perdiste'">Perdiste 😞</h3>
      <h3 v-else>Empate 🤝</h3>
      <div class="buttons">
        <button @click="resetGame" class="reset-button">Volver al inicio</button>
        <button @click="goToSelection" class="play-again-button">Otra vez</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      gameState: 'initial', // Estados: 'initial', 'selection', 'result'
      playerChoice: null,
      computerChoice: null,
      result: null,
      choices: ['piedra', 'papel', 'tijeras'],
    };
  },
  methods: {
    startGame() {
      this.gameState = 'selection';
    },
    play(choice) {
      this.playerChoice = choice;
      this.computerChoice = this.choices[Math.floor(Math.random() * this.choices.length)];
      this.determineWinner();
      this.gameState = 'result';
    },
    determineWinner() {
      if (this.playerChoice === this.computerChoice) {
        this.result = 'empate';
      } else if (
        (this.playerChoice === 'piedra' && this.computerChoice === 'tijeras') ||
        (this.playerChoice === 'papel' && this.computerChoice === 'piedra') ||
        (this.playerChoice === 'tijeras' && this.computerChoice === 'papel')
      ) {
        this.result = 'ganaste';
      } else {
        this.result = 'perdiste';
      }
    },
    resetGame() {
      this.gameState = 'initial';
      this.playerChoice = null;
      this.computerChoice = null;
      this.result = null;
    },
    goToSelection() {
      this.gameState = 'selection';
      this.playerChoice = null;
      this.computerChoice = null;
      this.result = null;
    },
  },
};
</script>

<style>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  font-family: "Eras ITC", sans-serif;
  background-color: rgb(0, 140, 255);
  margin: 0;
  border: 20px solid black;
  border-radius: 50px;
  height: 92.5vh;
}

.initial-screen,
.selection-screen {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 20px;
  margin-top: 30vh;
}

.play-button {
  padding: 15px 30px;
  font-size: 1.5em;
  border: none;
  border-radius: 8px;
  background-color: rgb(255, 0, 255);
  color: white;
  cursor: pointer;
  transition: background-color 0.3s ease;
  font-family: "Eras ITC", sans-serif;
}

.play-button:hover {
  background-color: rgb(0, 0, 0);
}

.choices {
  display: flex;
  gap: 15px;
}

.choice-button {
  padding: 12px 25px;
  font-size: 1.2em;
  border: 1px solid #ccc;
  border-radius: 5px;
  background-color: #f8f8f8;
  cursor: pointer;
  transition: background-color 0.3s ease;
  font-family: "Eras ITC", sans-serif;
}

.choice-button:hover {
  background-color: rgb(255, 0, 255);
}

.result-screen p {
  font-size: 1.1em;
}

.result-screen h3 {
  margin-top: 10px;
}

.buttons {
  display: flex;
  gap: 15px;
  margin-top: 20px;
}

.reset-button,
.play-again-button {
  padding: 10px 20px;
  font-size: 1em;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s ease;
  font-family: "Eras ITC", sans-serif;
}

.reset-button {
  background-color: black;
  color: white;
}

.reset-button:hover {
  background-color: magenta;
}

.play-again-button {
  background-color: white;
  color: rgb(255, 0, 255);
}

.play-again-button:hover {
  background-color: black;
}

.result-screen {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 20px;
  margin-top: 20vh;
}
</style>