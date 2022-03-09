<script setup>
import Head from "./components/Head.vue";
import Keyboard from "./components/Keyboard.vue";
import Gamestate from "./components/Gamestate.vue";
import Guessboard from "./components/Guessboard.vue";
</script>

<template>
  <header>
    <Head></Head>
  </header>

  <main>
    <h1>{{ letter }}</h1>
    <Guessboard :guessWord="guessWord"></Guessboard>
    <Gamestate :nbFail="nbFail"></Gamestate>
  </main>

  <footer>
    <Keyboard @typed="typed"></Keyboard>
  </footer>
</template>

<script>
export default {
  data() {
    return {
      secretWord: [],
      guessWord: [],
      nbFail: 0,
      letter: "_",
    }
  },
  methods: {
    typed(key) {
      if (key == "ok") {
        this.checkLetter()
      }
      else {
        this.letter = key
      }
    },
    checkLetter() {
      var found = false;
      if (this.letter != "_") {
        for (let i = 0; i < this.secretWord.length; i++) {
          const secretLetter = this.secretWord[i];
          if (secretLetter == this.letter) {
            this.guessWord[i] = secretLetter
            found = true
          }
        }
        if (found == false) {
          this.nbFail++;
        }
        this.letter = "_"
      }
    }
  },
  created() {
    this.secretWord = ["c", "h", "e", "r", "i", "e"];
    this.guessWord = new Array(this.secretWord.length);
    this.guessWord.fill("_");
  }
}

</script>
<style>
</style>
