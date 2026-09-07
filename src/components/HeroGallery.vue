<script setup>
import { onMounted, onUnmounted, ref } from 'vue'
import equipment from '../assets/hero/equipment.png'
import supplies from '../assets/hero/supplies.png'
import pills from '../assets/hero/pills.png'
import storage from '../assets/hero/storage.png'
import professional from '../assets/hero/professional.png'

const slides = [
  { src: equipment, alt: 'Medical monitoring equipment' },
  { src: supplies, alt: 'Shelved medical supplies' },
  { src: pills, alt: 'Pharmacist holding a pill bottle' },
  { src: storage, alt: 'Hospital storage corridor' },
  { src: professional, alt: 'Healthcare professional' },
]

// 5 sets to guarantee seamless infinite wrapping across wide screens
const loopSlides = [...slides, ...slides, ...slides, ...slides, ...slides]

const containerRef = ref(null)
const trackRef = ref(null)

// Config parameters
const BASE_SPEED = 32 // smooth pixels per second
let speed = BASE_SPEED
let offset = 0
let frameId = 0
let lastTime = 0

// Dimensions (responsive)
let cardWidth = 290
let cardHeight = 345
let gap = 12
let step = cardWidth + gap
let cycleWidth = slides.length * step
let baseCenterOffset = 12 * step
let cylinderRadius = 1500
let perspectiveVal = 1350

// Drag / touch interaction state
let isDragging = false
let startPointerX = 0
let dragStartOffset = 0
let lastPointerX = 0
let lastPointerTime = 0
let velocity = 0
let isHovered = false

function updateDimensions() {
  if (typeof window === 'undefined') return
  const w = window.innerWidth
  if (w < 640) {
    cardWidth = 195
    cardHeight = 240
    gap = 8
    cylinderRadius = 850
    perspectiveVal = 880
  } else if (w < 1024) {
    cardWidth = 240
    cardHeight = 290
    gap = 10
    cylinderRadius = 1150
    perspectiveVal = 1100
  } else {
    cardWidth = 290
    cardHeight = 345
    gap = 12
    cylinderRadius = 1500
    perspectiveVal = 1350
  }
  step = cardWidth + gap
  cycleWidth = slides.length * step
  baseCenterOffset = 12 * step

  if (offset === 0) {
    offset = baseCenterOffset
  }
}

function render() {
  if (!trackRef.value) return

  const nodes = trackRef.value.children
  const halfCard = cardWidth / 2
  const visibleThreshold = (typeof window !== 'undefined' ? window.innerWidth : 1400) / 2 + cardWidth + 80

  for (let i = 0; i < nodes.length; i++) {
    const node = nodes[i]
    // Distance from the carousel center
    const centerX = i * step - offset
    const absX = Math.abs(centerX)

    // Cull items far outside view
    if (absX > visibleThreshold) {
      node.style.display = 'none'
      continue
    }

    node.style.display = 'block'
    node.style.width = `${cardWidth}px`
    node.style.height = `${cardHeight}px`
    node.style.marginLeft = `${-halfCard}px`
    node.style.marginTop = `${-cardHeight / 2}px`

    // Cylindrical coordinates
    const theta = centerX / cylinderRadius // in radians
    const x = cylinderRadius * Math.sin(theta)
    const z = cylinderRadius * (Math.cos(theta) - 1)
    const rotateY = (theta * 180) / Math.PI

    node.style.transform = `translate3d(${x}px, 0px, ${z}px) rotateY(${rotateY}deg)`
    node.style.zIndex = String(Math.round(1000 - absX))
  }
}

function tick(time) {
  if (!lastTime) lastTime = time
  const dt = Math.min(0.05, (time - lastTime) / 1000)
  lastTime = time

  if (!isDragging) {
    // Momentum damping after drag release
    if (Math.abs(velocity) > 0.5) {
      offset += velocity * dt
      velocity *= Math.pow(0.05, dt) // smooth friction decay
    } else {
      velocity = 0
      const targetSpeed = isHovered ? 0 : BASE_SPEED
      speed += (targetSpeed - speed) * Math.min(1, dt * 8)
      offset += speed * dt
    }

    // Infinite loop normalization around center
    if (offset >= baseCenterOffset + cycleWidth) {
      offset -= cycleWidth
    } else if (offset < baseCenterOffset - cycleWidth) {
      offset += cycleWidth
    }
  }

  render()
  frameId = requestAnimationFrame(tick)
}

function onPointerDown(e) {
  isDragging = true
  startPointerX = e.clientX
  dragStartOffset = offset
  lastPointerX = e.clientX
  lastPointerTime = performance.now()
  velocity = 0
  if (containerRef.value) {
    containerRef.value.setPointerCapture?.(e.pointerId)
  }
}

function onPointerMove(e) {
  if (!isDragging) return
  const currentX = e.clientX
  const now = performance.now()
  const dt = (now - lastPointerTime) / 1000

  const dx = currentX - startPointerX
  offset = dragStartOffset - dx

  if (dt > 0.008) {
    velocity = (lastPointerX - currentX) / dt
    lastPointerX = currentX
    lastPointerTime = now
  }

  // Seamless wrap during drag
  if (offset >= baseCenterOffset + cycleWidth) {
    offset -= cycleWidth
    dragStartOffset -= cycleWidth
  } else if (offset < baseCenterOffset - cycleWidth) {
    offset += cycleWidth
    dragStartOffset += cycleWidth
  }

  render()
}

function onPointerUp(e) {
  if (!isDragging) return
  isDragging = false
  if (containerRef.value) {
    try {
      containerRef.value.releasePointerCapture?.(e.pointerId)
    } catch {}
  }
}

function onMouseEnter() {
  isHovered = true
}

function onMouseLeave() {
  isHovered = false
}

function onResize() {
  updateDimensions()
  render()
}

onMounted(() => {
  updateDimensions()
  offset = baseCenterOffset
  render()
  window.addEventListener('resize', onResize)
  frameId = requestAnimationFrame(tick)
})

onUnmounted(() => {
  cancelAnimationFrame(frameId)
  if (typeof window !== 'undefined') {
    window.removeEventListener('resize', onResize)
  }
})
</script>

<template>
  <div class="carousel-outer relative mt-10 w-screen left-1/2 -translate-x-1/2 overflow-hidden py-4 select-none md:mt-14">
    <div
      ref="containerRef"
      class="carousel-viewport relative w-full flex items-center justify-center cursor-grab active:cursor-grabbing touch-pan-y"
      :style="{ perspective: `${perspectiveVal}px` }"
      @pointerdown="onPointerDown"
      @pointermove="onPointerMove"
      @pointerup="onPointerUp"
      @pointercancel="onPointerUp"
      @mouseenter="onMouseEnter"
      @mouseleave="onMouseLeave"
    >
      <div
        class="carousel-stage relative w-full flex items-center justify-center"
        :style="{ height: `${cardHeight + 40}px` }"
      >
        <div
          ref="trackRef"
          class="carousel-track absolute top-1/2 left-1/2 w-0 h-0"
          style="transform-style: preserve-3d;"
        >
          <figure
            v-for="(slide, index) in loopSlides"
            :key="`${slide.alt}-${index}`"
            class="carousel-card absolute top-0 left-0 overflow-hidden rounded-[4px] bg-[#ebe7df] shadow-[0_4px_16px_rgba(20,30,25,0.06)] will-change-transform"
            style="transform-style: preserve-3d; backface-visibility: hidden;"
          >
            <img
              :src="slide.src"
              :alt="slide.alt"
              class="h-full w-full object-cover pointer-events-none select-none"
              draggable="false"
              loading="eager"
            />
          </figure>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.carousel-viewport {
  perspective-origin: 50% 50%;
  -webkit-font-smoothing: antialiased;
}

.carousel-stage {
  transform-style: preserve-3d;
}

.carousel-card {
  transform-origin: 50% 50%;
}
</style>


