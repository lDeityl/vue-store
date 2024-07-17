<script setup>

import Card from './Card.vue'

defineProps({
    items: Array,
});

</script>

<template>

    <div class="grid grid-cols-4 gap-5">
        <Card v-for="item in items" :key="item.id" :title="item.title" :price="item.price" :image-url="item.imageUrl"
            :is-favourite="item.isFavourite" />
    </div>

</template>