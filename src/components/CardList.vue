<script setup>
import Card from './Card.vue'

const onClickAdd = () => {
    alert('21312312');
}

</script>

<template>
    <div class="grid grid-cols-4 gap-5">
        <Card title="Мужские Кроссовки Nike Blazer Mid Suede" :price="1205" image-url="/sneakers/sneakers-1.jpg"
            :onClickAdd="onClickAdd" />
    </div>
</template>