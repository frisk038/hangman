<template>
    <div class="head">
        <button class="leadBtn" />
        <h1>WORSONE</h1>
        <button class="helpBtn" @click.self="$emit('needHelp')" />
    </div>
    <div class="sep">
        <hr />
    </div>
</template>

<script>
export default {
    emits: ['needHelp'],
}
</script>

<style>
.leadBtn {
    background: url("./icons/leaderboard.png") no-repeat;
    background-size: cover;
    width: 50px;
    height: 50px;
    border-radius: 10px;
    display: flex;
}
.helpBtn {
    background: url("./icons/help.png") no-repeat;
    background-size: cover;
    width: 50px;
    height: 50px;
    border-radius: 10px;
    display: flex;
}
.head {
    width: 360px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin: 5px;
}
.sep {
    width: 100%;
}
</style>
