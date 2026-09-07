<script setup>
import equipment from '../assets/hero/equipment.png'
import supplies from '../assets/hero/supplies.png'
import pills from '../assets/hero/pills.png'
import storage from '../assets/hero/storage.png'
import professional from '../assets/hero/professional.png'

const images = [
  {
    src: equipment,
    alt: 'Medical monitoring equipment',
    lift: 'mt-10 md:mt-14',
    tilt: '-rotate-[2.5deg]',
    delay: '0ms',
  },
  {
    src: supplies,
    alt: 'Shelved medical supplies',
    lift: 'mt-4 md:mt-6',
    tilt: '-rotate-[1deg]',
    delay: '90ms',
  },
  {
    src: pills,
    alt: 'Pharmacist holding a pill bottle',
    lift: 'mt-0',
    tilt: 'rotate-0',
    delay: '180ms',
  },
  {
    src: storage,
    alt: 'Hospital storage corridor',
    lift: 'mt-4 md:mt-6',
    tilt: 'rotate-[1deg]',
    delay: '270ms',
    showDot: true,
  },
  {
    src: professional,
    alt: 'Healthcare professional',
    lift: 'mt-10 md:mt-14',
    tilt: 'rotate-[2.5deg]',
    delay: '360ms',
  },
]
</script>

<template>
  <div class="relative mx-auto mt-14 w-full max-w-[1180px] px-3 md:mt-16 md:px-4">
    <div class="flex items-start justify-center gap-2 sm:gap-3 md:gap-4">
      <div
        v-for="image in images"
        :key="image.alt"
        class="animate-gallery-in relative w-[18.5%] min-w-[70px] max-w-[188px] shrink-0"
        :class="image.lift"
        :style="{ animationDelay: image.delay }"
      >
        <span
          v-if="image.showDot"
          class="absolute -top-3 right-3 z-10 h-2 w-2 rounded-full bg-accent"
          aria-hidden="true"
        />
        <figure
          class="overflow-hidden rounded-[1.1rem] shadow-[0_14px_32px_rgba(26,26,26,0.09)] transition duration-500 hover:-translate-y-1.5 hover:shadow-[0_20px_42px_rgba(26,26,26,0.14)]"
          :class="image.tilt"
        >
          <img
            :src="image.src"
            :alt="image.alt"
            class="aspect-[3/4] h-full w-full object-cover"
            loading="lazy"
          />
        </figure>
      </div>
    </div>
  </div>
</template>
