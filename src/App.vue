<script setup>
import { onMounted, reactive, ref, watch } from 'vue';
import axios from 'axios';

import Header from './components/Header.vue'
import CardList from './components/CardList.vue'
import Drawer from './components/Drawer.vue'

const items = ref([]); // { value: [] }

const filters = reactive({
    sortBy: 'title',
    searchQuery: ''
});

const onChangeSelect = e => {
    filters.sortBy = e.target.value;
}

const onChangeSearchInput = e => {
    filters.searchQuery = e.target.value;
}

const fetchItems = async () => {

    try {

        const params = {
            sortBy: filters.sortBy,
        }

        if (filters.searchQuery) {
            params.title = `*${filters.searchQuery}*`;
        }

        const { data } = await axios.get(`https://20a00b2442988ca5.mokky.dev/items`, {
            params
        });

        items.value = data;
    } catch (e) {
        console.log(e);
    }

}

onMounted(fetchItems); // useEffect(() => { }, [ ])

watch(filters, fetchItems);

</script>

<template>
    <!-- <Drawer /> -->
    <div class="bg-white w-4/5 m-auto  rounded-xl shadow-xl mt-14">
        <Header />

        <div class="p-10">
            <div class="flex justify-between items-center">
                <h2 class="text-3xl font-bold mb-8">Все кроссовки</h2>
                <div class="flex items-center gap-4">
                    <select @change="onChangeSelect" class="py-2 px-3 border rounded-md outline-none">
                        <option value="name">По названию</option>
                        <option value="price">По цене (дешёвые)</option>
                        <option value="-price">По цене (дорогие)</option>
                    </select>
                    <div class="relative">
                        <img class="absolute left-4 top-3" src="/search.svg" alt="icon">
                        <input @input="onChangeSearchInput"
                            class="border rounded-md py-2 pl-11 pr-4 outline-none focus:border-gray-400" type="text"
                            placeholder="Поиск...">
                    </div>
                </div>
            </div>
        </div>
        <CardList :items="items" />
    </div>
</template>