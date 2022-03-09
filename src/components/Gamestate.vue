<template>
    <div class="gamestate">
        <h1>{{ smileyState }}</h1>
    </div>
</template>

<script>
export default {
    data() {
        return {
        }
    },
    props: ['nbFail'],
    computed: {
        smileyState() {
            switch (this.nbFail) {
                case 0:

                    return '😄 . . . . . . . . . . 🐍';
                    break;
                case 1:
                    return '  😅 . . . . . . . . . 🐍';
                    break;
                case 2:
                    return '    🙂 . . . . . . . . 🐍';
                    break;
                case 3:
                    return '      🥲 . . . . . . . 🐍';
                    break;
                case 4:
                    return '        😐 . . . . . . 🐍';
                    break;
                case 5:
                    return '          🙁 . . . . . 🐍';
                    break;
                case 6:
                    return '            😦 . . . . 🐍';
                    break;
                case 7:
                    return '              😰 . . . 🐍';
                    break;
                case 8:
                    return '                😱 . . 🐍';
                    break;
                case 9:
                    return '                  😖 . 🐍';
                    break;
                case 10:
                    return '                       💀';
                    break;
                default:
                    break;
            }
        }
    }

}
</script>
<style>
.gamestate {
    width: 360px;
    height: 150px;
    display: flex;
    justify-content: center;
}
</style>
