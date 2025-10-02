<template>
  <nav class="bg-green-600 text-white">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="flex items-center justify-between h-16">
        <div class="flex items-center">
          <RouterLink to="/" class="flex items-center gap-2">
            <img src="../assets/logo.png" alt="Logo" class="h-8 w-8 rounded-4xl bg-white/10" />
            <span class="font-semibold text-3xl">Green Bean</span>
          </RouterLink>
        </div>

        <div class="flex sm:hidden">
          <button
            type="button"
            @click="open = !open"
            :aria-expanded="open.toString()"
            aria-label="Toggle navigation"
            class="inline-flex items-center justify-center p-2 rounded-md text-white hover:bg-white/10 focus:outline-none focus:ring-2 focus:ring-white"
          >
            <svg v-if="!open" class="h-6 w-6" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16"/>
            </svg>
            <svg v-else class="h-6 w-6" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"/>
            </svg>
          </button>
        </div>

        <div class="hidden sm:flex sm:items-center sm:space-x-8">
          <div class="flex space-x-2 text-lg font-bold">
            <RouterLink class="hover:bg-gray-900/40 hover:text-white/90 px-2 py-1 rounded-lg" to="/">Home</RouterLink>
            <RouterLink class="hover:bg-gray-900/40 hover:text-white/90 px-2 py-1 rounded-lg" to="/about">About</RouterLink>
            <RouterLink class="hover:bg-gray-900/40 hover:text-white/90 px-2 py-1 rounded-lg" to="/menu">Menu</RouterLink>
            <RouterLink class="hover:bg-gray-900/40 hover:text-white/90 px-2 py-1 rounded-lg" to="/testimonials">Testimonials</RouterLink>
          </div>

          <div class="ml-6 flex items-center space-x-3 text-lg font-bold">
            <RouterLink to="/signup" class="bg-white text-green-600 px-3 py-1.5 rounded-md font-semibold hover:opacity-90">Sign up</RouterLink>
            <RouterLink to="/login" class="text-white/95 hover:bg-gray-900/40 px-2 py-1 rounded-lg">Log in</RouterLink>
          </div>
        </div>
      </div>
    </div>

    <transition name="fade">
      <div v-show="open" class="sm:hidden bg-green-700/95 border-t border-green-800">
        <div class="px-4 pt-3 pb-4 space-y-1 text-lg font-bold">
          <RouterLink class="block px-3 py-2 rounded-md text-base font-medium text-white hover:bg-white/10" to="/">Home</RouterLink>
          <RouterLink class="block px-3 py-2 rounded-md text-base font-medium text-white hover:bg-white/10" to="/about">About</RouterLink>
          <RouterLink class="block px-3 py-2 rounded-md text-base font-medium text-white hover:bg-white/10" to="/menu">Menu</RouterLink>
          <RouterLink class="block px-3 py-2 rounded-md text-base font-medium text-white hover:bg-white/10" to="/testimonials">Testimonials</RouterLink>

          <div class="mt-2 border-t border-green-800 pt-3 text-lg font-bold">
            <RouterLink class="block w-full text-center bg-white text-green-600 px-3 py-2 rounded-md font-semibold mb-2" to="/signup">Sign up</RouterLink>
            <RouterLink class="block w-full text-center text-white/95 px-3 py-2 rounded-md" to="/login">Log in</RouterLink>
          </div>
        </div>
      </div>
    </transition>
  </nav>
</template>

<script setup>
import { ref } from 'vue';
import { RouterLink } from 'vue-router';

const open = ref(false);
</script>

<style scoped>
.fade-enter-active, .fade-leave-active {
  transition: opacity 150ms ease;
}
.fade-enter-from, .fade-leave-to {
  opacity: 0;
}
</style>
