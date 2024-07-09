<script setup>

import { ref } from 'vue'

const count = ref(0);

const inc = () => count.value++;

const dis = () => count.value--;

</script>

<template>
    <h1>{{ count }}</h1>
    <button @click="inc">+</button>
    <button @click="dis">-</button>
</template>
