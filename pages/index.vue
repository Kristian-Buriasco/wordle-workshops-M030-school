<template>
  <v-row justify="center" align="center">
    <v-col cols="12" sm="8" md="6">
      <v-card>
        <v-card-title class="headline">
          Step 4
        </v-card-title>
        <v-card-text>
          <div>
            <Guess class="mb-2" v-for="(guess, i) in board" :key="i" :guess="guess" :word="word"/>
          </div>
          <Input @guess="handleGuess"  />

          <!-- TODO: mostrare la parola corretta in caso di sconfitta -->
          <v-alert v-if="gameOver" type="error" class="mt-4">
            Hai perso! La parola era: {{word}}
          </v-alert>
          <!-- TODO: aggiungere pulsante "Gioca di nuovo" che usa il metodo reset() visibile quando si verifica lo stato gameOver -->
          <v-btn v-if="gameOver" @click="reset" class="mt-4" color="primary" large block>Gioca di nuovo</v-btn>
        </v-card-text>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
import { getRandomWord } from '~/utils/words';

export default {
  data: () => ({
    guesses: [],
    word: '',
  }),
  fetch() {
    
    this.word = getRandomWord().toUpperCase()
    console.log(this.word)
  },
  computed: {
    board() {
      // TODO (opzionale) mostrare sempre la board completa con 6 righe
      return this.guesses.concat(['', '', '', '', '', '']).slice(0, 6)
    },
    gameOver() {
      // TODO restituire true quando il gioco è finito: il gioco finisce se indovini la parola o raggiungi 6 tentativi
      if(this.guesses.length === 6) return true
      return false
    },
  },
  methods: {
    handleGuess(guess) {
      // TODO: aggiungere all'array di guesses il nuovo tentativo
      this.guesses.push(guess)
    },
    reset() {
      // TODO: implementare il reset del gioco
      this.guesses = []
      this.word = getRandomWord().toUpperCase()

    },
  }
}
</script>
