<script setup>
import Testimonials from '../components/Testimonials.vue';
</script>

<template>
    <Testimonials :reviews="sample" :limit="6" />
</template>