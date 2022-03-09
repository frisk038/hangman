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

                    return '😄 _ _ _ _ _ _ _ _ _ _ 🐍';
                    break;
                case 1:
                    return '  😅 _ _ _ _ _ _ _ _ _ 🐍';
                    break;
                case 2:
                    return '    🙂 _ _ _ _ _ _ _ _ 🐍';
                    break;
                case 3:
                    return '      🥲 _ _ _ _ _ _ _ 🐍';
                    break;
                case 4:
                    return '        😐 _ _ _ _ _ _ 🐍';
                    break;
                case 5:
                    return '          🙁 _ _ _ _ _ 🐍';
                    break;
                case 6:
                    return '            😦 _ _ _ _ 🐍';
                    break;
                case 7:
                    return '              😰 _ _ _ 🐍';
                    break;
                case 8:
                    return '                😱 _ _ 🐍';
                    break;
                case 9:
                    return '                  😖 _ 🐍';
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
    width: 500px;
    display: flex;
    justify-content: center;
}
</style>
