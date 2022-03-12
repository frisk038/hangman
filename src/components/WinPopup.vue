<template>
    <div class="modal-backdrop">
        <div class="modal">
            <section class="modal-body">
                <div v-if="nbFail != 10">
                    <h1>Félicitations 🎉</h1>
                    <div class="wintext">
                        <h3>Bravo, tu as gagné! Reviens demain pour un nouveau défi.</h3>
                        <h4>
                            Tu peux aussi entrer ton pseudo pour la gloire
                            <br />(3 chiffres/lettres max.)
                        </h4>
                    </div>

                    <div class="username" v-on:submit.prevent="onSubmit">
                        <form class="unform">
                            <div class="inputtextdiv">
                                <input
                                    v-model="username"
                                    type="text"
                                    maxlength="3"
                                    pattern="[a-zA-Z0-9-]+"
                                    class="userinput"
                                    onkeyup="
                            var start = this.selectionStart;
                            var end = this.selectionEnd;
                            this.value = this.value.toUpperCase();
                            this.setSelectionRange(start, end);"
                                    required
                                />
                            </div>
                            <div class="submitdiv">
                                <button class="submit"></button>
                            </div>
                        </form>
                    </div>
                </div>
                <div v-else>
                    <h1>Perdu 🥺</h1>
                    <div class="wintext">
                        <h4>Arf, dommage! Retente ta chance demain!</h4>
                        <h4>Le mot secret était : {{ mergedWord }}</h4>
                        <br />
                    </div>
                </div>

                <div class="sharediv">
                    <h4>Copie ta partie pour la partager, garantie sans spoil.</h4>
                    <div class="sharebtndiv">
                        <button v-on:click="generateClipboard" class="sharebtn"></button>
                    </div>
                </div>
            </section>
        </div>
    </div>
</template>

<script>
export default {
    props: ['nbFail', 'mergedWord'],
    data() {
        return {
            username: ""
        }
    },
    methods: {
        generateClipboard() {
            var text = "Poisoned\n\n"
            switch (this.nbFail) {
                case 0:
                    text += "A fini avec tout ces PV !\n"
                    text += "🟩🟩🟩🟩🟩🟩🟩🟩🟩🟩 100%\n\n"
                    break;
                case 1:
                    text += "Bravo !\n"
                    text += "🟩🟩🟩🟩🟩🟩🟩🟩🟩⬜️  90%\n\n"
                    break;
                case 2:
                    text += "Bravo !\n"
                    text += "🟩🟩🟩🟩🟩🟩🟩🟩⬜️⬜️  80%\n\n"
                    break;
                case 3:
                    text += "Bravo !\n"
                    text += "🟩🟩🟩🟩🟩🟩🟩⬜️⬜️⬜️  70%\n\n"
                    break;
                case 4:
                    text += "A transpiré...\n"
                    text += "🟨🟨🟨🟨🟨🟨⬜️⬜️⬜️⬜️  60%\n\n"
                    break;
                case 5:
                    text += "A transpiré...\n"
                    text += "🟨🟨🟨🟨🟨⬜️⬜️⬜️⬜️⬜️  50%\n\n"
                    break;
                case 6:
                    text += "A transpiré...\n"
                    text += "🟧🟧🟧🟧⬜️⬜️⬜️⬜️⬜️⬜️  40%\n\n"
                    break;
                case 7:
                    text += "A transpiré...\n"
                    text += "🟧🟧🟧⬜️⬜️⬜️⬜️⬜️⬜️⬜️  30%\n\n"
                    break;
                case 8:
                    text += "A eu chaud aux fesses !\n"
                    text += "🟥🟥⬜️⬜️⬜️⬜️⬜️⬜️⬜️⬜️  20%\n\n"
                    break;
                case 9:
                    text += "A glissé !\n"
                    text += "🟥⬜️⬜️⬜️⬜️⬜️⬜️⬜️⬜️⬜️  10%\n\n"
                    break;
                case 10:
                    text += "A cassé sa pipe !\n"
                    text += "⬜️⬜️⬜️⬜️⬜️⬜️⬜️⬜️⬜️⬜️  0%\n\n"
                    break;
            }
            text += '\nhttps://poisoned.netlify.app'
            this.copyToClipboard(text)
        },
        async copyToClipboard(mytext) {
            try {
                await navigator.clipboard.writeText(mytext);
                alert("C'est copié");
            } catch ($e) {
                alert('Oups y a une erreur');
            }
        },
        onSubmit() {
            console.log(this.username)
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
    text-align: center;
}

.sharebtn {
    background: url("./icons/clipboard.png") no-repeat;
    width: 50px;
    height: 50px;
    background-size: cover;
    border-radius: 10px;
}
</style>
