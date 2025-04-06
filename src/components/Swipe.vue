<template>
  <div class="flex flex-col items-center justify-center min-h-screen bg-gray-100">
    <div v-if="showRetry" class="m-6 text-red-500">Wrong direction. Try again!</div>
    <div class="flex items-center gap-4 lg:gap-[60px]" v-if="!testCompleted">
      <button @click="() => handleDirection('left')" class="px-4 py-2 h-[40px] bg-blue-500 text-white rounded-lg shadow">Swipe Left</button>
      <div class="relative w-80 h-96">
        <transition name="fade">
          <div
            v-if="currentCard"
            :key="currentIndex"
            class="absolute inset-0 bg-white rounded-2xl shadow-xl flex items-center justify-center text-xl font-bold text-gray-700"
          >
            {{ currentCard.text }}
          </div>
        </transition>
      </div>
      <button @click="() => handleDirection('right')" class="px-4 py-2 h-[40px] bg-green-500 text-white rounded-lg shadow">Swipe Right</button>
    </div>
    <div v-else class="w-80 h-96 flex items-center justify-center bg-white rounded-2xl shadow-xl text-2xl font-semibold text-green-600">Great Job!</div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';

const cards = ref([
  { text: "Swipe me right", correctDirection: "right" },
  { text: "Swipe me left", correctDirection: "left" },
  { text: "Again to the right", correctDirection: "right" },
]);

const currentIndex = ref(0);
const showRetry = ref(false);
const testCompleted = ref(false);

const currentCard = computed(() => cards.value[currentIndex.value] || null);

const handleDirection = (direction) => {
  const correct = currentCard.value.correctDirection;
  if (direction === correct) {
    showRetry.value = false;
    currentIndex.value++;
    if (currentIndex.value >= cards.value.length) {
      testCompleted.value = true;
    }
  } else {
    showRetry.value = true;
  }
};
</script>

<style>
.fade-enter-active, .fade-leave-active {
  transition: opacity 0.3s ease;
}
.fade-enter, .fade-leave-to {
  opacity: 0;
}
</style>
