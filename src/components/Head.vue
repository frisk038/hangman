<template>
<div class="head">
    <button class="leadBtn" />
    <h1>WORSONE</h1>
    <button class="helpBtn" />
</div>
</template>

<script>
export default {

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
    width: 600px;
    display: flex;
    align-items: flex-start;
    justify-content: space-between;
    margin: 5px;
}
</style>
