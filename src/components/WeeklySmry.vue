<template>
    <div @click.self="$emit('closeWeeklySmry')" class="modal-backdrop">
        <div class="modal">
            <section class="modal-body">
                <div>
                    <div class="wintext">
                        <h1>Bravo !</h1>
                        <h4>Le champion 🏆 de la semaine est :</h4>
                        🎉 <span class="username"> {{ this.weeklyBestPlayer.user_name }} </span> avec {{ this.weeklyBestPlayer.score }} points 🎊
                        <br /><br />
                        <div class="gifdiv">
                            <img class="gif" :src=this.gifUrl />
                        </div>
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
            gifUrl: "empty"
        }
    },
    methods: {
        async getWinGif() {
            try {
                let response = await fetch("https://hangman-poisoned.herokuapp.com/wingif");
                if (response.status == 200) {
                    var gif = await response.json();
                    this.gifUrl = gif.url
                }

            } catch (error) {
                console.log(error);
            }
        },
    },
    created() {
        this.getWinGif()
    }
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
    border-radius: 20px;
}

.modal-body {
    position: relative;
    padding: 20px 5px;
    color: #ffffff;
}

.username {
    font-size: 150%;
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

.gifdiv {
    display: flex;
    flex-flow: column;
    align-items: center;
}
.gif {
    width: 50%;
    height: 20%;
}

</style>
