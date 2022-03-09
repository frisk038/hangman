<template>
    <div @click.self="$emit('closeHelp')" class="modal-backdrop">
        <div class="modal">
            <section class="modal-body">
                <h1>Règles 🥸</h1>
                <span>
                    <div>
                        Un seul mot secret par jour, à vous de le deviner !
                        <br />Vous avez pour cela 10 petits tours avant de se faire piquer par le serpent 🐍
                    </div>
                    <br />Bonne chance 🤞 !
                    <div class="closeDiv">
                        <button @click="$emit('closeHelp')">C'est parti !</button>
                    </div>
                </span>
            </section>
        </div>
    </div>
</template>

<script>
export default {
    emits: ['closeHelp'],
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
}

.modal-body {
    position: relative;
    padding: 20px 5px;
    color: #ffffff;
}

.closeDiv {
    width: 100%;
    text-align: right;
}
</style>
