<script setup>
import  Card from '@/components/Card.vue'
import { ref } from 'vue';

const cards = ref([
  {
    id: 1,
    title: 'Steam',
    description: 'This is the first card.',
  },
  {
    id: 2,
    title: 'Water',
    description: 'This is the second card.',
  },
  {
    id: 3,
    title: 'Ice',
    description: 'This is the third card.',
  },
  {
    id: 4,
    title: 'Lightening',
    description: 'This is the fourth card.',
  },

]);

const scrollToSection = () => {
  const section = document.getElementById('section-two');
  section?.scrollIntoView({ behavior: 'smooth' });
};
</script>

<template>
  <div id="section-one" class="bg-gray-100 p-[10px] flex flex-col items-center justify-center">
    <h1 class="font-sans font-bold p-4 lg:text-xl">Tap to Discover State of Matter!</h1>
    <div
    class="w-2/5 lg:w-1/4 mx-auto grid grid-cols-1 md:grid-cols-2 gap-6 justify-evenly content-center place-content-center relative overflow-hidden"
  >
  <Card 
  v-for="card in cards" 
  :key="card.id"
  :id="card.id"
  :title="card.title"
  :description="card.description"
  />
    </div>
    <button @click="scrollToSection" class="px-4 py-2 my-[40px] h-[40px] bg-blue-500 text-white rounded-lg shadow">Next</button>
  </div>

</template>
