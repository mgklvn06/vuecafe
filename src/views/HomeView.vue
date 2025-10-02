<script setup>
import Hero from '../components/Hero.vue';
import About from '../components/About.vue';
import Menu from '../components/Menu.vue';
import Testimonials from '../components/Testimonials.vue';
</script>

<template>
    <Hero />
    <About />
    <Menu :limit="6" :showButton="true" />
    <Testimonials :reviews="sample" :limit="6" />
</template>