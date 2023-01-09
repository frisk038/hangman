<template>
    <div id="app">

        <Particles id="tsparticles" :particlesInit="particlesInit" :particlesLoaded="particlesLoaded" :options="{
    fpsLimit: 120,
    particles: {
        color: {
            value: '#fff'
        },
        move: {
            direction: 'bottom',
            enable: true,
            outMode: 'out',
            speed: 2,
        },
        number: {
            density: {
                enable: true,
                area: 3000
            },
            value: 400
        },
        opacity: {
            value: 0.7
        },
        shape: {
            type: 'char',
            character: [
                {
                    fill: true,
                    font: 'Verdana',
                    value: ['💩', '🤡', '🍀', '🍙'],
                    style: '',
                    weight: 400
                }
            ]
        },
        size: {
            random: true,
            value: 8
        },
        zIndex: {
            value: {
                min: 0,
                max: 100
            }
        }
    },
    detectRetina: true
}" />
    </div>
</template>


<script>
import { loadFull } from "tsparticles";

const particlesInit = async engine => {
    await loadFull(engine);
};

const particlesLoaded = async container => {
    console.log("Particles container loaded", container);
};

export default {
    data() {
        return {
            particlesInit,
            particlesLoaded,
        }
    },
}
</script>

<style>

</style>