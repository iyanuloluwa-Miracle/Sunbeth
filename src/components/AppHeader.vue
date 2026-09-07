<script setup>
</script>

<template>
  <header class="w-full">
    <div class="mx-auto flex max-w-[1180px] items-center justify-between px-6 py-5 md:px-10">
      <a href="/" class="leading-none" aria-label="Sunbeth Healthcare">
        <span class="block text-[1.35rem] font-extrabold tracking-tight text-brand md:text-[1.5rem]">
          Sunbeth
        </span>
        <span class="block text-[1.35rem] font-extrabold tracking-tight text-accent md:text-[1.5rem]">
          Healthcare
        </span>
      </a>

      <nav class="flex items-center gap-5 md:gap-8" aria-label="Primary">
        <a
          href="#about"
          class="hidden text-[0.95rem] font-medium text-ink transition hover:text-brand sm:inline"
        >
          About Sunbeth
        </a>

        <button
          type="button"
          class="inline-flex items-center gap-1.5 text-[0.95rem] font-medium text-ink transition hover:text-brand"
          aria-label="Language: English"
        >
          <svg
            class="h-[18px] w-[18px]"
            viewBox="0 0 24 24"
            fill="none"
            stroke="currentColor"
            stroke-width="1.8"
            aria-hidden="true"
          >
            <circle cx="12" cy="12" r="9" />
            <path d="M3 12h18M12 3c2.5 2.8 3.8 5.8 3.8 9s-1.3 6.2-3.8 9c-2.5-2.8-3.8-5.8-3.8-9S9.5 5.8 12 3z" />
          </svg>
          <span>EN</span>
          <svg
            class="h-3.5 w-3.5"
            viewBox="0 0 12 12"
            fill="none"
            stroke="currentColor"
            stroke-width="1.8"
            aria-hidden="true"
          >
            <path d="M2.5 4.5 6 8l3.5-3.5" stroke-linecap="round" stroke-linejoin="round" />
          </svg>
        </button>

        <a
          href="#contact"
          class="inline-flex items-center rounded-full border border-brand px-5 py-2 text-[0.9rem] font-semibold text-brand transition hover:bg-brand hover:text-white"
        >
          Get in Touch
        </a>
      </nav>
    </div>

    <div class="mx-auto max-w-[1180px] border-b border-line px-6 md:px-10"></div>
  </header>
</template>
