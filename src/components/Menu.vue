<script setup>
import { ref, computed, onMounted } from 'vue';
import axios from 'axios';

const props = defineProps({
  limit: Number,
  showButton: {
    type: Boolean,
    default: false
  }
});

const menu = ref([]);
const expanded = ref(false);
const loading = ref(true);  
const error = ref(null);     
const searchQuery = ref(''); 

const initialLimit = computed(() => {
  return typeof props.limit === 'number' ? props.limit : menu.value.length;
});

const filteredMenu = computed(() => {
  if (!searchQuery.value) return menu.value;
  return menu.value.filter(item =>
    item.title.toLowerCase().includes(searchQuery.value.toLowerCase()) ||
    item.description.toLowerCase().includes(searchQuery.value.toLowerCase())
  );
});

const displayed = computed(() => {
  return expanded.value ? filteredMenu.value : filteredMenu.value.slice(0, initialLimit.value);
});

const toggleExpanded = () => {
  expanded.value = !expanded.value;
};

const formatPrice = (p) => {
  return `Kshs${Number(p).toFixed(2)}`;
};

const fetchMenu = async () => {
  loading.value = true;
  error.value = null;
  try {
    const response = await axios.get('http://localhost:3000/menu');
    menu.value = response.data.menu || response.data; 
  } catch (err) {
    error.value = 'Failed to load menu. Please check your network and try again.';
    console.error('Error fetching menu data:', err);
  } finally {
    loading.value = false;
  }
};

onMounted(fetchMenu);
</script>

<template>
  <section class="w-full max-w-7xl mx-auto px-6 py-12">
    <header class="mb-8 text-center">
      <h2 class="text-3xl font-extrabold text-green-800">Our Menu</h2>
      <p class="mt-2 text-gray-600">Handcrafted beverages and fresh pastries made daily.</p>
    </header>

    <div class="flex justify-center mb-8">
      <input
        v-model="searchQuery"
        type="text"
        placeholder="Search menu..."
        class="w-full max-w-md px-4 py-2 border border-gray-300 rounded-l-md focus:ring-2 focus:ring-green-400 focus:outline-none"
      />
      <button
        @click="() => {}"
        class="px-4 py-2 bg-green-600 text-white rounded-r-md hover:bg-green-700"
      >
        Search
      </button>
    </div>

    <div v-if="loading" class="flex justify-center items-center py-20">
      <svg class="animate-spin h-10 w-10 text-green-700" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24">
        <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"/>
        <path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8v8H4z"/>
      </svg>
      <span class="ml-3 text-gray-600">Loading menu...</span>
    </div>

    <div v-else-if="error" class="text-center py-10">
      <p class="text-red-600 mb-4">{{ error }}</p>
      <button
        @click="fetchMenu"
        class="px-6 py-3 bg-green-600 text-white rounded-md hover:bg-green-700 focus:outline-none"
      >
        Retry
      </button>
    </div>

    <div v-else-if="!loading && filteredMenu.length === 0" class="text-center py-10 text-gray-500">
      No menu items found.
    </div>

    <div v-else class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6">
      <article
        v-for="item in displayed"
        :key="item.id"
        class="bg-white rounded-lg shadow-sm overflow-hidden flex flex-col justify-between"
        role="article"
        :aria-labelledby="`menu-item-${item.id}`"
      >
        <div class="w-full h-44 sm:h-40 lg:h-48 bg-gray-100 overflow-hidden">
          <img
            v-if="item.image"
            :src="item.image"
            :alt="item.imageAlt || item.title"
            loading="lazy"
            class="w-full h-full object-cover"
          />
          <div v-else class="w-full h-full flex items-center justify-center text-gray-400">
            No image
          </div>
        </div>

        <div class="p-6">
          <div class="flex items-start justify-between">
            <h3 :id="`menu-item-${item.id}`" class="text-lg font-bold text-green-800">
              {{ item.title }}
            </h3>
            <div class="text-green-700 font-semibold text-sm">
              {{ formatPrice(item.price) }}
            </div>
          </div>

          <p class="mt-3 text-sm text-gray-700">
            {{ item.description }}
          </p>
        </div>

        <div class="p-4 border-t border-gray-100 flex items-center justify-end gap-3">
          <a
            :href="item.orderButton?.url || '#'"
            class="inline-flex items-center gap-2 bg-green-600 text-white px-4 py-2 rounded-md text-sm font-medium hover:bg-green-700 focus:outline-none focus:ring-2 focus:ring-green-300"
            :aria-label="`Order ${item.title}`"
          >
            {{ item.orderButton?.text || 'Order' }}
          </a>
        </div>
      </article>
    </div>

    <div v-if="!loading && !error && props.showButton && filteredMenu.length > initialLimit" class="m-auto max-w-sm my-10 px-8 text-center">
      <button
        @click="toggleExpanded"
        class="w-full inline-flex justify-center items-center gap-2 bg-gray-900 text-white py-3 px-6 rounded-xl hover:bg-gray-950 focus:outline-none focus:ring-2 focus:ring-green-300"
        :aria-expanded="expanded.toString()"
      >
        <span v-if="!expanded">Load more</span>
        <span v-else>Show less</span>
      </button>
    </div>
  </section>
</template>

<style scoped>
article:hover {
  transform: translateY(-4px);
  transition: transform 160ms ease;
}
</style>
