<template>
    <div @click.self="$emit('closeWeeklySmry')" class="modal-backdrop">
        <div class="modal">
            <section class="modal-body">
                <div>
                    <h1>Bonne semaine !</h1>
                    <div class="wintext">
                        <h1>Félicitations au champion de la semaine 🏆</h1>
                        <h1>🎉 {{ this.weeklyBestPlayer.user_name }} avec un score de {{this.weeklyBestPlayer.score}} points 🎊</h1>
                        <br />
                    </div>
                </div>

                <div class="sharediv">
                    <div class="btndiv">
                        <div class="closebtndiv">
                            <button @click="$emit('closeWeeklySmry')" class="closebtn"></button>
                        </div>
                    </div>
                </div>
            </section>
        </div>
    </div>
</template>

<script>
export default {
    props: ['weeklyBestPlayer'],
    emits: ['closeWeeklySmry'],
    data() {
        return {
            winner: ""
        }
    },
};
</script>

 <style scoped>
.modal-backdrop {
    position: fixed;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    background-color: rgba(0, 0, 0, 0.6);
    display: flex;
    justify-content: center;
    align-items: center;
}

.modal {
    background: #474747;
    box-shadow: 2px 2px 200px 1px;
    width: 95%;
}

.modal-body {
    position: relative;
    padding: 20px 5px;
    color: #ffffff;
}

.username {
    display: flex;
    justify-content: center;
    height: 50px;
}

.unform {
    width: 30%;
    display: flex;
    justify-content: space-around;
}

.inputtextdiv {
    display: flex;
    align-items: center;
}
.userinput {
    width: 50px;
    height: 20px;
    text-align: center;
    font-size: 16px;
}

.submitdiv {
    display: flex;
    align-items: center;
}
.submit {
    background: url("./icons/check.png") no-repeat;
    width: 40px;
    height: 40px;
    background-size: cover;
    border-radius: 10px;
}

.wintext {
    text-align: center;
}

.sharediv {
    display: flex;
    flex-flow: column;
    align-items: center;
    text-align: center;
}

.sharebtn {
    background: url("./icons/clipboard.png") no-repeat;
    width: 50px;
    height: 50px;
    background-size: cover;
    border-radius: 10px;
}

.closebtn {
    background: url("./icons/cancel.png") no-repeat;
    width: 50px;
    height: 50px;
    background-size: cover;
    border-radius: 10px;
}
.btndiv {
    width: 200px;
    display: flex;
    justify-content: space-around;
}
</style>
