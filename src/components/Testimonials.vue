<template>
  <section class="max-w-7xl mx-auto px-6 py-12">
    <header class="mb-8 text-center">
      <h2 class="text-3xl font-extrabold text-green-800">What customers say</h2>
      <p class="mt-2 text-gray-600">Real reviews from our friendly customers.</p>
    </header>

    <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6">
      <article
        v-for="r in displayed"
        :key="r.id"
        class="bg-white rounded-xl shadow-sm p-6 flex flex-col"
        role="article"
        :aria-labelledby="`review-${r.id}-name`"
      >
        <div class="flex items-start gap-4">
          <img
            :src="person"
            class="h-14 w-14 rounded-full object-cover flex-shrink-0"
            loading="lazy"
          />
          <div class="flex-1">
            <div class="flex items-center justify-between">
              <div>
                <h3 :id="`review-${r.id}-name`" class="text-sm font-semibold text-green-800">
                  {{ r.name }}
                </h3>
                <p class="text-xs text-gray-500 mt-0.5">{{ r.when }}</p>
              </div>

              <div class="flex items-center" :aria-label="`Rating: ${r.rating} out of 5`">
                <svg
                  v-for="n in 5"
                  :key="n"
                  class="h-5 w-5"
                  :class="n <= r.rating ? 'text-yellow-400' : 'text-gray-300'"
                  viewBox="0 0 20 20"
                  fill="currentColor"
                  aria-hidden="true"
                >
                  <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.286 3.97a1 1 0 00.95.69h4.18c.969 0 1.371 1.24.588 1.81l-3.388 2.462a1 1 0 00-.364 1.118l1.287 3.97c.3.922-.755 1.688-1.54 1.118L10 13.347l-3.489 2.58c-.785.57-1.84-.196-1.54-1.118l1.287-3.97a1 1 0 00-.364-1.118L2.507 9.397c-.783-.57-.38-1.81.588-1.81h4.18a1 1 0 00.95-.69l1.286-3.97z" />
                </svg>
              </div>
            </div>

            <p class="mt-4 text-gray-700 text-sm leading-relaxed">
              {{ r.text }}
            </p>
          </div>
        </div>

        <footer class="mt-6 pt-4 border-t border-gray-100 text-sm text-gray-500">
          <span class="font-medium text-green-700">{{ r.recommend ? 'Recommended' : 'Reviewed' }}</span>
          <span class="mx-2">·</span>
          <span>{{ r.location || 'Local customer' }}</span>
        </footer>
      </article>
    </div>
  </section>
</template>

<script setup>
import { computed } from 'vue';
import person from '../assets/person.png';

const props = defineProps({
  reviews: {
    type: Array,
    default: null
  },
  limit: {
    type: Number,
    default: 6
  }
});

const sample = [
  {
    id: 1,
    name: 'Aisha Mwangi',
    rating: 5,
    text: 'Lovely coffee and a very cozy atmosphere. The matcha latte is my favorite — perfectly balanced.',
    when: '2 weeks ago',
    recommend: true,
    location: 'Nairobi'
  },
  {
    id: 2,
    name: 'John Otieno',
    rating: 5,
    text: 'Great service and freshly baked croissants. Will come back for the cold brew.',
    when: '1 month ago',
    recommend: true,
    location: 'Nairobi'
  },
  {
    id: 3,
    name: 'Sophie Kim',
    rating: 4,
    text: 'Nice workspace and reliable wifi. Coffee could be a bit stronger for my taste.',
    when: '3 days ago',
    recommend: true,
    location: 'Mombasa'
  },
  {
    id: 4,
    name: 'Daniel N.',
    rating: 4,
    text: 'Friendly staff and fast orders. Pastries are fresh every morning.',
    when: 'Yesterday',
    recommend: true,
    location: 'Kisumu'
  },
  {
    id: 5,
    name: 'Lina Patel',
    rating: 5,
    text: 'Beautiful interior and delicious seasonal sandwich. Highly recommend the cappuccino.',
    when: '2 months ago',
    recommend: true,
    location: 'Nairobi'
  },
  {
    id: 6,
    name: 'Mark R.',
    rating: 3,
    text: 'Good coffee but it was a bit busy — service slowed down. Food was tasty though.',
    when: '3 weeks ago',
    recommend: false,
    location: 'Nakuru'
  }
];

const displayed = computed(() => {
  const list = props.reviews && props.reviews.length ? props.reviews : sample;
  return list.slice(0, props.limit);
});
</script>

<style scoped>
article:hover { transform: translateY(-6px); transition: transform 180ms ease; }
</style>