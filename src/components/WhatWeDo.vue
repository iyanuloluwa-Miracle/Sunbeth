<script setup>
import pharmaceuticals from '../assets/pharmaceuticals.jpg'
import medicalDevices from '../assets/medical_devices.jpg'

const services = [
  {
    id: 'pharmaceuticals',
    image: pharmaceuticals,
    alt: 'Pharmaceutical products including vials and medicine bottles',
    title: 'Pharmaceuticals',
    description: 'Quality pharmaceutical products supporting better health outcomes.',
  },
  {
    id: 'medical-devices',
    image: medicalDevices,
    alt: 'Medical diagnostic equipment being operated by a gloved professional',
    title: 'Medical Devices & Diagnostics',
    description: 'Advanced equipment and solutions enabling accurate, timely healthcare delivery.',
  },
]
</script>

<template>
  <section class="what-we-do-section" aria-labelledby="what-we-do-heading">
    <!-- Section label -->
    <div class="section-label">
      <span class="label-dot" aria-hidden="true"></span>
      <span class="label-text">WHAT WE DO</span>
    </div>

    <!-- Heading -->
    <h2 id="what-we-do-heading" class="section-heading">
      Healthcare solutions backed<br />
      by the strength of Sunbeth.
    </h2>

    <!-- Cards grid -->
    <div class="cards-grid">
      <article
        v-for="service in services"
        :key="service.id"
        class="service-card"
      >
        <div class="card-image-wrapper">
          <img
            :src="service.image"
            :alt="service.alt"
            class="card-image"
            loading="lazy"
          />
        </div>
        <div class="card-body">
          <h3 class="card-title">{{ service.title }}</h3>
          <p class="card-description">{{ service.description }}</p>
        </div>
      </article>
    </div>
  </section>
</template>

<style scoped>
.what-we-do-section {
  max-width: 1180px;
  margin: 0 auto;
  padding: 72px 24px 80px;
  text-align: center;
}

@media (min-width: 768px) {
  .what-we-do-section {
    padding-left: 40px;
    padding-right: 40px;
  }
}

/* ── Label ─────────────────────────────────────────── */
.section-label {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  margin-bottom: 20px;
}

.label-dot {
  display: inline-block;
  width: 8px;
  height: 8px;
  border-radius: 50%;
  background: #3cb371;
  flex-shrink: 0;
}

.label-text {
  font-size: 11px;
  font-weight: 700;
  letter-spacing: 0.12em;
  color: #1a1a1a;
  text-transform: uppercase;
}

/* ── Heading ────────────────────────────────────────── */
.section-heading {
  font-size: clamp(28px, 4vw, 42px);
  font-weight: 500;
  line-height: 1.25;
  color: #1a2520;
  letter-spacing: -0.02em;
  margin: 0 0 52px;
}

/* ── Cards Grid ─────────────────────────────────────── */
.cards-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 24px;
  text-align: left;
}

@media (max-width: 640px) {
  .cards-grid {
    grid-template-columns: 1fr;
  }
}

/* ── Individual Card ────────────────────────────────── */
.service-card {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.card-image-wrapper {
  width: 100%;
  aspect-ratio: 4 / 3;
  border-radius: 16px;
  overflow: hidden;
  background: #e8e4db;
}

.card-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
  transition: transform 0.5s cubic-bezier(0.22, 1, 0.36, 1);
}

.service-card:hover .card-image {
  transform: scale(1.04);
}

/* ── Card Body ──────────────────────────────────────── */
.card-body {
  padding: 0 4px;
}

.card-title {
  font-size: 18px;
  font-weight: 700;
  color: #1b6b45;
  margin: 0 0 8px;
  letter-spacing: -0.01em;
}

.card-description {
  font-size: 14px;
  line-height: 1.65;
  color: #4a4a4a;
  margin: 0;
  max-width: 340px;
}
</style>
