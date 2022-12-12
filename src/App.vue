<script setup>
import { ref, computed } from 'vue';
import VerovioScore from './components/VerovioScore.vue'
const meiFiles = [
    'https://raw.githubusercontent.com/WolfgangDrescher/lassus-geistliche-psalmen/master/kern/01-beatus-vir.krn',
    'https://raw.githubusercontent.com/WolfgangDrescher/lassus-geistliche-psalmen/master/kern/02-quare-fremuerunt-gentes.krn',
    'https://raw.githubusercontent.com/WolfgangDrescher/lassus-geistliche-psalmen/master/kern/03-domine-quid-multiplicati.krn',
    'https://raw.githubusercontent.com/WolfgangDrescher/lassus-geistliche-psalmen/master/kern/04-cum-invocarem.krn',
];

const num = ref(0);

function loadScores() {
    num.value += 10;
    console.log(scoreNumbers.value);
}

const scoreNumbers = computed(() => {
    return [...Array(10).keys()].map(x => x + num.value);
});
</script>

<template>
    <button @click="loadScores">Load 10 scores</button>
    <template v-for="n in scoreNumbers" :key="n">
        <h1>{{ n }}</h1>
        <VerovioScore :url="meiFiles[n % meiFiles.length]" />
    </template>
</template>
