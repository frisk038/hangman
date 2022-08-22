<script setup>
import { v4 as uuidv4 } from 'uuid';
import confetti from 'canvas-confetti'
import Head from "./components/Head.vue";
import Keyboard from "./components/Keyboard.vue";
import Gamestate from "./components/Gamestate.vue";
import Guessboard from "./components/Guessboard.vue";
import HelpPopup from "./components/HelpPopup.vue";
import WinPopup from "./components/WinPopup.vue";
import Ranking from "./components/Ranking.vue";
import WeeklySmry from './components/WeeklySmry.vue';
</script>

<template>
  <HelpPopup v-if="helpRequired" @closeHelp="helpRequired = false"></HelpPopup>
  <Ranking v-if="rankingRequired" @closeRanking="rankingRequired = false" :ranking="ranking"></Ranking>
  <WinPopup v-if="gameState != 0 && showWinPopup" :nbFail="nbFail" :mergedWord="mergedWord"
    :cookieUserName="cookieUserName" @saveUser="saveUser" @closeWinPopup="showWinPopup = false"></WinPopup>
  <WeeklySmry v-if="showWeeklySmry" @closeWeeklySmry="showWeeklySmry = false" :weeklyBestPlayer="weeklyBestPlayer"></WeeklySmry>

  <div class="headr">
    <Head @needHelp="helpRequired = true" @showRanking="rankingRequired = true" :secretNumber="secretNumber"></Head>
  </div>
  
  <div class="username" v-if="cookieUserName != ''">Hey {{ cookieUserName }} 👋🏾</div>
  <div class="game">
    <div class="guessword">
      <h1>{{ letter }}</h1>
    </div>
    <Guessboard :guessWord="guessWord"></Guessboard>
    <Gamestate :nbFail="nbFail"></Gamestate>
    <Keyboard @typed="typed" :letter="letter" :secretNumber="secretNumber"></Keyboard>
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
      ranking: [],
      weeklyBestPlayer: "toto",
      showWeeklySmry: false
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
      if (this.letter != "_" && this.secretNumber != 0) {
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
          this.saveScore()
        } else if (!this.guessWord.includes("_")) {
          this.gameState = 1
          this.saveScore()
          confetti({
            particleCount: 100,
            spread: 100,
            origin: { x: 0.5, y: 0.8 }
          });
        }
        this.storeGameState()
      }
    },
    storeGameState() {
      let date = new Date();
      var midnight = new Date(date.getFullYear(), date.getMonth(), date.getDate(), 23, 59, 59);
      setCookieAndExpire("gamestate", this.gameState, midnight)
      setCookieAndExpire("nbfail", this.nbFail, midnight)
      setCookieAndExpire("guessword", JSON.stringify(this.guessWord), midnight)
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
      var gword = getCookie("guessword")
      if (gword != "") {
        this.guessWord = JSON.parse(gword)
        console.log(this.guessWord)
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
              'user_name': this.cookieUserName,
              'user_agent': navigator.userAgent
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
          this.ranking = secretJs.leaderboard
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
    },
    async getWeeklyTopPlayer() {
      try {
        let response = await fetch("https://hangman-poisoned.herokuapp.com/top?secretnb=" + (this.secretNumber-1));
        var secretJs = await response.json();
        if (secretJs.status == "Ok")  {
          this.weeklyBestPlayer = secretJs.leaderboard[0]
        }
      } catch (error) {
        console.log(error);
      }
    },
    async checkWeeklySmry() {
      let date = new Date()
      if (!this.helpRequired && getCookie("gamestate") == "" && date.getDay() == 7) {
        await this.getWeeklyTopPlayer();
        this.showWeeklySmry = true;
         confetti({
            particleCount: 100,
            spread: 100,
            origin: { x: 0.5, y: 0.8 }
          });
      }
    },
  },
  async created() {
    await this.getSecret();
    this.getTopPlayer();
    this.readGameState();
    this.checkWeeklySmry();
  },
  mounted() {
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
