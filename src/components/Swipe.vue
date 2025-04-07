<template>
  <div id="section-two" class="flex flex-col items-center justify-center min-h-screen bg-gray-100">
    <div v-if="showRetry" class="m-6 text-red-500">Wrong direction. Try again!</div>
    <div class="flex items-center gap-4 lg:gap-[60px] m-[10px]" v-if="!testCompleted">
      <button @click="() => handleDirection('left')" class="text-sm p-2 lg-text-md lg:px-4 py-2 min-h-[40px] bg-blue-500 text-white rounded-lg shadow">Swipe Left</button>
      <div class="relative w-40 h-52 lg:w-80 lg:h-96">
        <transition name="fade">
          <div
            v-if="currentCard"
            :key="currentIndex"
            class="absolute inset-0 bg-white rounded-2xl shadow-xl flex items-center text-center justify-center font-bold text-gray-700 text-md lg:text-xl p-3"
          >
            {{ currentCard.text }}
          </div>
        </transition>
      </div>
      <button @click="() => handleDirection('right')" class="text-sm p-2 lg-text-md lg:px-4 py-2 min-h-[40px] bg-green-500 text-white rounded-lg shadow">Swipe Right</button>
    </div>
    <div v-else class="w-80 h-96 flex items-center justify-center bg-white rounded-2xl shadow-xl text-2xl font-semibold text-green-600">Great Job!</div>
    <div v-else class="flex flex-col items-center gap-4">
      <h3 class="text-2xl my-[40px] font-semibold text-green-600">Test Completed!</h3>
      <button @click="resetGame" class="px-6 py-2 text-sm bg-gray-100 shadow-md text-gray rounded-lg">Try Again</button>
      <button @click="scrollToSection" class="px-4 py-2 my-[40px] h-[40px] bg-blue-500 text-white rounded-lg shadow">Next</button>
    </div>

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


const resetGame = () => {
  currentIndex.value = 0;
  showRetry.value = false;
  testCompleted.value = false;
};

const scrollToSection = () => {
  const section = document.getElementById('section-one');
  section?.scrollIntoView({ behavior: 'smooth' });
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
