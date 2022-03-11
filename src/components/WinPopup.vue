<template>
    <div class="modal-backdrop">
        <div class="modal">
            <section class="modal-body">
                <div v-if="nbFail != 10">
                    <h1>Félicitations 🎉</h1>
                    <span>Bravo, tu as gagné! Reviens demain pour un nouveau défi.</span>
                </div>
                <div v-else>
                    <h1>Perdu 🥺</h1>
                    <span>Le mot secret était : {{ mergedWord }}</span>
                    <br />
                    <span>Arf, dommage! Retente ta chance demain!</span>
                </div>

                <div class="share">
                    <button v-on:click="generateClipboard">Partage ta partie</button>
                </div>
            </section>
        </div>
    </div>
</template>

<script>
export default {
    props: ['nbFail', 'mergedWord'],
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
                    text += "Il a transpiré...\n"
                    text += "🟨🟨🟨🟨🟨🟨⬜️⬜️⬜️⬜️  60%\n\n"
                    break;
                case 5:
                    text += "Il a transpiré...\n"
                    text += "🟨🟨🟨🟨🟨⬜️⬜️⬜️⬜️⬜️  50%\n\n"
                    break;
                case 6:
                    text += "Il a transpiré...\n"
                    text += "🟧🟧🟧🟧⬜️⬜️⬜️⬜️⬜️⬜️  40%\n\n"
                    break;
                case 7:
                    text += "Il a transpiré...\n"
                    text += "🟧🟧🟧⬜️⬜️⬜️⬜️⬜️⬜️⬜️  30%\n\n"
                    break;
                case 8:
                    text += "A eu chaud aux fesses !\n"
                    text += "🟥🟥⬜️⬜️⬜️⬜️⬜️⬜️⬜️⬜️  20%\n\n"
                    break;
                case 9:
                    text += "A eu chaud aux fesses !\n"
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

.share {
    margin: 0 auto;
    text-align: center;
}

.shareTab {
    margin: 0 auto;
    text-align: center;
}
</style>
