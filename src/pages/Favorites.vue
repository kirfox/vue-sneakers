<script setup>
import { ref, onMounted } from 'vue'
import axios from 'axios'
import CardList from '../components/CardList.vue'
const favorites = ref([])
const emit = defineEmits(['addToFavorite', 'addToCart']);


onMounted(async () => {
    try {
        const { data } = await axios.get('https://8575360c0f94d94b.mokky.dev/favorites?_relations=items')
        favorites.value = data.map(obj => obj.item)
    } catch (error) {
        console.log(error)
    }
})
</script>


<template>
    <h2 class="text-3xl font-bold mb-8">Мои закладки</h2>
    <div class="mt-10">
        <CardList 
        :items="favorites" is-favorites ></CardList>
    </div>
</template>