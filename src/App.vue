<script setup>
import Head from "./components/Head.vue";
import Keyboard from "./components/Keyboard.vue";
import Gameboard from "./components/Gameboard.vue";
</script>

<template>
  <header>
    <Head></Head>
  </header>

  <main></main>

  <footer>
    <Gameboard :nbFail="nbFail"></Gameboard>
    <Keyboard @typed="typed"></Keyboard>
  </footer>
</template>

<script>
export default {
  data() {
    return {
      secretWord: "maison",
      nbFail: 0
    }
  },
  methods: {
    typed(key) {
      this.nbFail++;
      console.log(key)
    }
  }
}

</script>
<style>
</style>
