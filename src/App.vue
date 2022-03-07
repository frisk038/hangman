<script setup>
import Head from "./components/Head.vue";
import Keyboard from "./components/Keyboard.vue";
</script>

<template>
  <header>
    <Head></Head>
  </header>

  <main></main>

  <footer>
    <Keyboard @typed="typed"></Keyboard>
  </footer>
</template>

<script>
export default {
  methods: {
    typed(key) {
      console.log(key)
    }
  }
}

</script>
<style>
</style>
