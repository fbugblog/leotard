<script setup>
import AppHeader from './components/AppHeader.vue'
import HeroSection from './components/HeroSection.vue'
import ConceptSection from './components/ConceptSection.vue'
import ProgramsSection from './components/ProgramsSection.vue'
import FeaturesSection from './components/FeaturesSection.vue'
import ContactSection from './components/ContactSection.vue'
import AppFooter from './components/AppFooter.vue'
</script>

<template>
  <AppHeader />
  <main>
    <HeroSection />
    <ConceptSection />
    <ProgramsSection />
    <FeaturesSection />
    <ContactSection />
  </main>
  <AppFooter />
</template>
