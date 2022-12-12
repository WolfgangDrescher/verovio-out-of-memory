<script setup>
import { onMounted, onUnmounted, ref } from 'vue';
import createVerovioModule from 'verovio/wasm-hum';
import { VerovioToolkit } from 'verovio/esm';

const props = defineProps(['url']);

const svg = ref('');
const toolkit = ref();

onMounted(() => {
    createVerovioModule().then(async VerovioModule => {
        toolkit.value = new VerovioToolkit(VerovioModule);
        const response = await fetch(props.url);
        const kernScore = await response.text();
        toolkit.value.setOptions({
            scale: 15,
        });
        toolkit.value.loadData(kernScore);
        svg.value = toolkit.value.renderToSVG(1);
    });
});

onUnmounted(() => {
    toolkit.value.destroy();
});
</script>

<template>
    <div v-html="svg"></div>
</template>

