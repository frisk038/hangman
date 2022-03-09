<script setup>
import Head from "./components/Head.vue";
import Keyboard from "./components/Keyboard.vue";
import Gamestate from "./components/Gamestate.vue";
import Guessboard from "./components/Guessboard.vue";
import HelpPopup from "./components/HelpPopup.vue";
import WinPopup from "./components/WinPopup.vue";
</script>

<template>
  <HelpPopup v-show="helpRequired" @closeHelp="helpRequired = false"></HelpPopup>

  <WinPopup v-if="gameState != 0" :nbFail="nbFail"></WinPopup>
  <div class="headr">
    <Head @needHelp="helpRequired = true"></Head>
  </div>
  <div class="game">
    <div class="guessword">
      <h1>{{ letter }}</h1>
    </div>
    <Guessboard :guessWord="guessWord"></Guessboard>
    <Gamestate :nbFail="nbFail"></Gamestate>
    <Keyboard @typed="typed"></Keyboard>
  </div>
</template>

<script>
export default {
  data() {
    return {
      secretWord: [],
      guessWord: [],
      nbFail: 0,
      letter: "_",
      nbMaxPlay: 10,
      helpRequired: true,
      gameState: 0
    }
  },
  methods: {
    typed(key) {
      if (this.nbFail < this.nbMaxPlay) {
        if (key == "ok") {
          this.checkLetter()
        }
        else {
          this.letter = key
        }
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
        if (this.nbFail == this.nbMaxPlay) {
          this.gameState = -1
        } else if (!this.guessWord.includes("_")) {
          this.gameState = 1
        }
      }
    }
  },
  created() {
    this.secretWord = ["a", "n", "t", "i", "c", "o", "n", "s", "t", "i", "t", "u", "t"];
    this.guessWord = new Array(this.secretWord.length);
    this.guessWord.fill("_");
  }
}

</script>

<style>
.guessword {
  width: 50px;
  display: flex;
  justify-content: center;
}

.game {
  display: flex;
  flex-flow: column wrap;
  justify-content: center;
  align-content: center;
  align-items: center;
}

.headr {
  display: flex;
  justify-content: center;
  flex-flow: column wrap;
  justify-content: center;
  align-content: center;
  align-items: center;
}
</style>
