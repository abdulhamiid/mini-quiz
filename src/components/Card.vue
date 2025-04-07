<script setup>
import { ArrowUturnLeftIcon } from "@heroicons/vue/24/outline";
import { SparklesIcon } from "@heroicons/vue/24/solid";
import { ref, defineProps } from "vue";
const isFlipped = ref(false);

const flipCard = () => {
  isFlipped.value = !isFlipped.value;
};

  defineProps({
    title: {
      type: String,
    },
    description: {
      type: String,
    },
  })
</script>

<template>
  <div class="flex w-full items-center">

    <!-- Main Container Of Card -->

    <div
      :class="{ flipped: isFlipped }"
      class="flip-container relative h-52 w-full rounded-3xl"
    >
      <!-- Front Side Of Card -->

      <div
        class="flip-card-front absolute left-0 top-0 z-10 flex h-full w-full items-center justify-center rounded-3xl bg-gradient-to-br from-orange-500 to-pink-500 p-6 text-center text-white transition-all duration-[1000ms] ease-in-out"
      >
        <h2 class="font-sans text-lg text-white font-bold">{{ title }}</h2>
        <button
          @click="flipCard()"
          tabindex="0"
          class="absolute bottom-0 right-2 animate-bounce rounded-full bg-white/90 p-2 text-orange-500"
        >
          <SparklesIcon class="size-6" />
        </button>
      </div>

      <!-- Back Side Of Card -->

      <div
        class="flip-card-back absolute left-0 top-0 z-0 flex h-full w-full flex-col items-center justify-center transition-all duration-[1000ms] ease-in-out"
      >
        <div
          class="relative flex h-full w-full flex-col items-center justify-center gap-6 rounded-3xl bg-white p-6 text-center text-black"
        >
          <Transition name="go-back">
            <button
              @click="flipCard()"
              tabindex="0"
              v-if="isFlipped"
              class="go-back absolute bottom-2 left-3 rounded-full bg-black/90 p-2 text-white transition-transform duration-300 hover:scale-110"
            >
              <ArrowUturnLeftIcon class="size-6" />
            </button>
          </Transition>

          <Transition name="info">
            <div v-if="isFlipped" class="mt-6 text-lg italic">
              {{description}}
            </div>
          </Transition>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
/* Adding Perspective To Parent Container */

.flip-container {
  perspective: 1000px;
}

/* Hiding The Back Of Card */

.flip-card-front,
.flip-card-back {
  backface-visibility: hidden;
}

/* Setting The Default Postion Of The Back Of The Card */

.flip-card-back {
  transform: rotateY(180deg);
}

/* If you want to flip the card using 'Hover' */

/* .flip-container:hover .flip-card-front {
  transform: rotateY(180deg);
}

.flip-container:hover .flip-card-back {
  transform: rotateY(360deg);
} */

/* Flipping The Card On Click */

.flip-container.flipped .flip-card-front {
  transform: rotateY(180deg);
}

.flip-container.flipped .flip-card-back {
  transform: rotateY(360deg);
}

/* Transition API Animations */

.about-enter-from,
.about-leave-to {
  scale: 0;
}
.about-enter-to,
.about-leave-from {
  scale: 1;
}
.about-enter-active,
.about-leave-active {
  transition: scale 0.5s ease-in;
  transition-delay: 1s;
}

.info-enter-from,
.info-leave-to,
.go-back-enter-from,
.go-back-leave-to {
  opacity: 0;
}

.info-enter-to,
.info-leave-from,
.go-back-enter-to,
.go-back-leave-from {
  opacity: 1;
}

.info-enter-active,
.info-leave-active {
  transition: opacity 1.5s ease-in;
}

.go-back-enter-active,
.go-back-leave-active {
  transition: opacity 0.5s ease-in;
}

</style>