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

  <WinPopup v-if="gameState != 0" :nbFail="nbFail" :mergedWord="mergedWord"></WinPopup>
  <div class="headr">
    <Head @needHelp="helpRequired = true" :secretNumber="secretNumber"></Head>
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
function setCookieToMidnight(cname, cvalue) {
  let date = new Date();
  var midnight = new Date(date.getFullYear(), date.getMonth(), date.getDate(), 23, 59, 59);
  document.cookie = cname + "=" + cvalue + ";expires=" + midnight.toUTCString();
}

function getCookie(cname) {
  let name = cname + "=";
  let ca = document.cookie.split(';');
  for(let i = 0; i < ca.length; i++) {
    let c = ca[i];
    while (c.charAt(0) == ' ') {
      c = c.substring(1);
    }
    if (c.indexOf(name) == 0) {
      return c.substring(name.length, c.length);
    }
  }
  return "";
}

function storeGameState() {
  this.setCookieToMidnight("gamestate", this.gameState)
  this.setCookieToMidnight("nbfail", this.nbFail)
}

function readGameState() {
  var state = this.getCookie("gamestate")
  if (state != "") {
    this.gameState = state
  }
  var fail = this.getCookie("nbfail")
  if (fail != "") {
    this.nbFail = fail
  }
}

export default {
  data() {
    return {
      secretWord: [],
      guessWord: [],
      nbFail: 0,
      letter: "_",
      nbMaxPlay: 10,
      helpRequired: true,
      gameState: 0,
      secretNumber: 0,
      mergedWord: ""
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
          this.storeGameState()
        } else if (!this.guessWord.includes("_")) {
          this.gameState = 1
          this.storeGameState()
        }
      }
    }
  },
  async created() {
    try {
      let response = await fetch("https://hangman-poisoned.herokuapp.com/getsecret");
      var secretJs = await response.json();
      this.secretWord = secretJs.secret;
      this.secretNumber = secretJs.number;
      this.guessWord = new Array(this.secretWord.length);
      this.guessWord.fill("_");
      this.secretWord.forEach(letter => {
        this.mergedWord += letter
      });
    } catch (error) {
      console.log(error);
    }
  },
  mounted(){
    this.readGameState()
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
