<script setup>
import { RouterLink } from 'vue-router';
import cafe1 from '../assets/cafe1.webp';
</script>

<template>
  <section
    role="img"
    aria-label="Cozy cafe interior with wooden tables and warm lighting"
    :style="{ backgroundImage: `url(${cafe1})` }"
    class="relative bg-cover bg-center min-h-[100vh] sm:min-h-[100vh] flex items-center"
  >
    <div class="absolute inset-0 bg-gradient-to-b from-green-800/60 via-green-700/40 to-black/30"></div>

    <div class="relative z-10 w-full max-w-7xl mx-auto px-6 py-16 sm:py-24 lg:py-32 text-white">
      <div class="max-w-2xl">
        <span class="inline-block bg-white/10 text-green-100 text-sm font-medium px-3 py-1 rounded-full mb-4">
          Family‑run • Fresh beans • Cozy vibes
        </span>

        <h1 class="mt-4 text-3xl sm:text-5xl font-extrabold leading-tight">
          Sip. Savor. Stay.
        </h1>

        <p class="mt-4 text-lg sm:text-xl text-white/90">
          Welcome to The Green Bean — your neighborhood cafe for hand‑crafted coffee, seasonal pastries, and a warm place to work or unwind. Locally roasted, ethically sourced, always delicious.
        </p>

        <div class="mt-8 flex flex-wrap gap-3">
          <RouterLink
            to="/menu"
            class="inline-flex items-center gap-2 bg-white text-green-700 px-4 py-2 rounded-md font-semibold shadow-sm hover:opacity-95 focus:outline-none focus:ring-2 focus:ring-white/40"
          >
            View Menu
          </RouterLink>

          <RouterLink
            to="/reserve"
            class="inline-flex items-center gap-2 border border-white/30 text-white px-4 py-2 rounded-md hover:bg-white/5 focus:outline-none focus:ring-2 focus:ring-white/30"
          >
            Reserve a Table
          </RouterLink>
        </div>

        <p class="mt-6 text-sm text-white/80">
          Open daily 7am — 8pm • Walk‑ins welcome
        </p>
      </div>
    </div>
  </section>
</template>

<style scoped>
a:hover { transition: opacity 120ms ease, background-color 120ms ease; }

@media (min-width: 1024px) {
  section[role="img"] { background-position: center 35%; }
}
</style>