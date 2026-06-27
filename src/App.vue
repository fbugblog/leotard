<script setup>
import AppHeader from './components/AppHeader.vue'
import HeroSection from './components/HeroSection.vue'
import ConceptSection from './components/ConceptSection.vue'
import ProductsSection from './components/ProductsSection.vue'
import FeaturesSection from './components/FeaturesSection.vue'
import TestimonialsSection from './components/TestimonialsSection.vue'
import ContactSection from './components/ContactSection.vue'
import AppFooter from './components/AppFooter.vue'
</script>

<template>
  <AppHeader />
  <main>
    <HeroSection />
    <ConceptSection />
    <ProductsSection />
    <FeaturesSection />
    <TestimonialsSection />
    <ContactSection />
  </main>
  <AppFooter />
</template>
