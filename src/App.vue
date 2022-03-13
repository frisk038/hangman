<script setup>
import { v4 as uuidv4 } from 'uuid';
import Head from "./components/Head.vue";
import Keyboard from "./components/Keyboard.vue";
import Gamestate from "./components/Gamestate.vue";
import Guessboard from "./components/Guessboard.vue";
import HelpPopup from "./components/HelpPopup.vue";
import WinPopup from "./components/WinPopup.vue";
import Ranking from "./components/Ranking.vue";
</script>

<template>
  <HelpPopup v-if="helpRequired" @closeHelp="helpRequired = false"></HelpPopup>
  <Ranking v-if="rankingRequired" @closeRanking="rankingRequired = false" :ranking="ranking"></Ranking>

  <WinPopup
    v-if="gameState != 0 && showWinPopup"
    :nbFail="nbFail"
    :mergedWord="mergedWord"
    :cookieUserName="cookieUserName"
    @saveUser="saveUser"
    @closeWinPopup="showWinPopup = false"
  ></WinPopup>

  <div class="headr">
    <Head
      @needHelp="helpRequired = true"
      @showRanking="rankingRequired = true"
      :secretNumber="secretNumber"
    ></Head>
  </div>
  <div class="username" v-if="cookieUserName != ''">Hey {{ cookieUserName }} 👋🏾</div>
  <div class="game">
    <div class="guessword">
      <h1>{{ letter }}</h1>
    </div>
    <Guessboard :guessWord="guessWord"></Guessboard>
    <Gamestate :nbFail="nbFail"></Gamestate>
    <Keyboard @typed="typed" :letter="letter"></Keyboard>
  </div>
</template>

<script>
function setCookieAndExpire(cname, cvalue, expire) {
  document.cookie = cname + "=" + cvalue + ";expires=" + expire.toUTCString();
}

function getCookie(cname) {
  let name = cname + "=";
  let ca = document.cookie.split(';');
  for (let i = 0; i < ca.length; i++) {
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

export default {
  data() {
    return {
      secretWord: [],
      guessWord: [],
      nbFail: 0,
      letter: "_",
      nbMaxPlay: 10,
      helpRequired: false,
      gameState: 0,
      secretNumber: 0,
      mergedWord: "",
      userID: "",
      cookieUserName: "",
      rankingRequired: false,
      showWinPopup: true,
      ranking: []
    }
  },
  methods: {
    typed(key) {
      if (this.gameState == 0) {
        if (this.nbFail < this.nbMaxPlay) {
          if (key == "ok") {
            this.checkLetter()
          }
          else {
            this.letter = key
          }
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
          this.saveScore()
        } else if (!this.guessWord.includes("_")) {
          this.gameState = 1
          this.storeGameState()
          this.saveScore()
        }
      }
    },
    storeGameState() {
      let date = new Date();
      var midnight = new Date(date.getFullYear(), date.getMonth(), date.getDate(), 23, 59, 59);
      setCookieAndExpire("gamestate", this.gameState, midnight)
      setCookieAndExpire("nbfail", this.nbFail, midnight)
    },
    readGameState() {
      var state = getCookie("gamestate")
      if (state != "") {
        this.gameState = parseInt(state)
      }
      var fail = getCookie("nbfail")
      if (fail != "") {
        this.nbFail = parseInt(fail)
      }
      var username = getCookie("username")
      if (username != "") {
        this.cookieUserName = username
        setCookieAndExpire("username", this.cookieUserName, new Date("2030/01/01"))
      }
    },
    setUserId() {
      this.userID = getCookie("userID")
      if (this.userID == "") {
        this.userID = uuidv4()
        this.helpRequired = true
      }
      var forEver = new Date("2030/01/01")
      setCookieAndExpire("userID", this.userID, forEver)
    },
    async saveScore() {
      try {
        let post = await fetch("https://hangman-poisoned.herokuapp.com/score",
          {
            method: "POST",
            headers: { 'Content-Type': 'text/plain' },
            body: JSON.stringify({
              'user_id': this.userID,
              'secret_num': this.secretNumber,
              'score': this.nbFail,
              'user_name': this.cookieUserName
            })
          })
      } catch (error) {
        console.log(error);
      }
    },
    async saveUser(username) {
      try {
        let post = await fetch("https://hangman-poisoned.herokuapp.com/user",
          {
            method: "POST",
            headers: { 'Content-Type': 'text/plain' },
            body: JSON.stringify({
              'user_id': this.userID,
              'secret_num': this.secretNumber,
              'user_name': username
            })
          })
        var response = await post.json();
        if (response.status == "Ok") {
          this.cookieUserName = username
          setCookieAndExpire("username", this.cookieUserName, new Date("2030/01/01"))
        } else {
          alert("Oups 🙇🏾‍♂️ ce pseudo est déjà pris !")
        }
      } catch (error) {
        console.log(error);
      }
    },
    async getTopPlayer() {
      try {
        let response = await fetch("https://hangman-poisoned.herokuapp.com/top?secretnb=" + this.secretNumber);
        var secretJs = await response.json();
        if (secretJs.status == "Ok") {
          this.ranking = []
          secretJs.leaderboard.forEach(topUser => {
            this.ranking.push({ name: topUser.user_name, score: 10 - topUser.score })
          });
        }
      } catch (error) {
        console.log(error);
      }
    },
    async getSecret() {
      try {
        let response = await fetch("https://hangman-poisoned.herokuapp.com/secret");
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
    }
  },
  async created() {
    await this.getSecret()
    this.getTopPlayer()
  },
  mounted() {
    this.readGameState();
    this.setUserId();
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
