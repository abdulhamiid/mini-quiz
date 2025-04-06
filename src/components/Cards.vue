<script setup>
import  Card from '@/components/Card.vue'
import { ref } from 'vue';

const cards = ref([
  {
    id: 1,
    title: 'Card 1',
    description: 'This is the first card.',
  },
  {
    id: 2,
    title: 'Card 2',
    description: 'This is the second card.',
  },
  {
    id: 3,
    title: 'Card 3',
    description: 'This is the third card.',
  },
  {
    id: 4,
    title: 'Card 4',
    description: 'This is the fourth card.',
  },

]);
</script>

<template>
   <div
    class="w-2/5 mx-auto m-[50px] grid grid-cols-2 gap-6 place-content-center relative overflow-hidden"
  >
  <Card 
  v-for="card in cards" 
  :key="card.id"
  :id="card.id"
  :title="card.title"
  :description="card.description"
  />
</div>

</template>
