<template>
<div class="gameboard">
    <table>
        <tr>
            <td v-for="(gw, idx) in guessWord" :key="idx"> <h1>{{ gw }}</h1></td>
        </tr>
    </table>
</div>
</template>

<script>
export default {
    props: ['guessWord'],
}
</script>

<style>
.gameboard{
    display: flex;
    width: 200px;
    justify-content: center;
}
</style>
