<script setup>
import HeroGallery from './HeroGallery.vue'
</script>

<template>
  <section class="mx-auto flex w-full max-w-[1180px] flex-col items-center px-6 pb-16 pt-14 text-center md:px-10 md:pb-20 md:pt-[4.5rem]">
    <h1
      class="animate-fade-up max-w-[940px] text-[2.05rem] font-bold leading-[1.12] tracking-[-0.03em] text-brand sm:text-[2.65rem] md:text-[3.45rem] lg:text-[3.85rem]"
      style="animation-delay: 60ms"
    >
      Advancing <span class="text-accent">Healthcare</span>
      <span class="block">Through Quality, Access</span>
      <span class="block">and Reliability.</span>
    </h1>

    <p
      class="animate-fade-up mt-6 max-w-[540px] text-[0.98rem] leading-[1.65] text-muted md:mt-7 md:text-[1.1rem]"
      style="animation-delay: 160ms"
    >
      Our network seamlessly connects global healthcare manufacturers by guaranteeing
      compliant medical products.
    </p>

    <a
      href="#partner"
          class="animate-fade-up group mt-9 inline-flex items-center gap-3 rounded-full bg-brand py-2.5 pl-6 pr-2.5 text-[0.95rem] font-semibold text-white shadow-[0_10px_24px_rgba(14,75,68,0.22)] transition hover:bg-[#0a3d37] hover:shadow-[0_14px_28px_rgba(14,75,68,0.28)] md:mt-10"
      style="animation-delay: 260ms"
    >
      Partner With Us
      <span
        class="inline-flex h-9 w-9 items-center justify-center rounded-full bg-brand-soft text-brand transition group-hover:translate-x-0.5"
        aria-hidden="true"
      >
        <svg class="h-4 w-4" viewBox="0 0 16 16" fill="none" stroke="currentColor" stroke-width="2.2">
          <path d="M3.5 8h9M8.5 4.5 12 8l-3.5 3.5" stroke-linecap="round" stroke-linejoin="round" />
        </svg>
      </span>
    </a>

    <HeroGallery />
  </section>
</template>
