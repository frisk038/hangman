<template>
    <div @click.self="$emit('closeRanking')" class="modal-backdrop">
        <div class="modal">
            <h1>Classement 📈</h1>
            <section class="modal-body">
                <div class="rankingdiv">
                    <h4>Voici les cinq premiers de la semaine !</h4>
                    <span class="numerouno" v-if="ranking[0] != null">🥇 {{ ranking[0].user_name }} avec un score de {{
                            ranking[0].score
                    }} points 🎉</span>
                    <br />
                    <span class="numerodos" v-if="ranking[1] != null">🥈 {{ ranking[1].user_name }} pas très loin avec
                        {{ ranking[1].score }} points 🥳</span>
                    <br />
                    <span class="numerotres" v-if="ranking[2] != null">🥉 {{ ranking[2].user_name }} sauve l'honneur à
                        {{ ranking[2].score }} points 🙌🏾</span>
                    <br />
                    <span class="numeroquatro" v-if="ranking[3] != null">🍪 {{ ranking[3].user_name }} y croit dur avec
                        {{ ranking[3].score }} points 🤞🏾</span>
                    <br />
                    <span class="numerocinqo" v-if="ranking[4] != null">🍫 {{ ranking[4].user_name }} s'accroche à ses
                        {{ ranking[4].score }} points 💪🏾</span>
                </div>
                <br />
                <div class="closeDiv">
                    <button @click="$emit('closeRanking')" class="closerankingbtn"></button>
                </div>
            </section>
        </div>
    </div>
</template>

<script>
export default {
    props: ['ranking'],
    emits: ['closeRanking'],
    data() {
        return {
        }
    },
};
</script>

 <style scoped>
.modal-backdrop {
    position: fixed;
    display: flex;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    background-color: rgba(0, 0, 0, 0.6);
    justify-content: center;
    align-items: center;
}

.modal {
    background: #474747;
    box-shadow: 2px 2px 200px 1px;
    width: 95%;
    display: flex;
    flex-flow: column;
    align-content: center;
    align-items: center;
    border-radius: 20px;
}

.modal-body {
    position: relative;
    padding: 20px 5px;
    color: #ffffff;
    display: flex;
    flex-flow: column;
    align-items: center;
    justify-content: space-around;
}

.rankingdiv {
    display: flex;
    flex-flow: column;
    align-items: center;
}

.closeDiv {
    display: flex;
    justify-content: center;
    width: 50%;
    height: 40px;
}

.closerankingbtn {
    background: url("./icons/cancel.png") no-repeat;
    width: 50px;
    height: 50px;
    background-size: cover;
    border-radius: 10px;
}
</style>
