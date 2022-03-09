<script setup>
import Head from "./components/Head.vue";
import Keyboard from "./components/Keyboard.vue";
import Gameboard from "./components/Gameboard.vue";
</script>

<template>
  <header>
    <Head></Head>
  </header>

  <main>
    <h1>{{ letter }}</h1>
    <Gameboard :nbFail="nbFail"></Gameboard>
  </main>

  <footer>
    <Keyboard @typed="typed"></Keyboard>
  </footer>
</template>

<script>
export default {
  data() {
    return {
      secretWord: "maison",
      nbFail: 0,
      letter: "_",
    }
  },
  methods: {
    typed(key) {
      this.nbFail++;
      this.letter = key
    }
  }
}

</script>
<style>
</style>
