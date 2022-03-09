<template>
    <table>
        <tr>
            <td v-for="(gw, idx) in guessWord" :key="idx">{{ gw }}</td>
        </tr>
    </table>
</template>

<script>
export default {
    props: ['guessWord'],
}
</script>

<style>
</style>