<template>
  <TheCursor />
  <TheNavbar :mob="mobOpen" @toggleMob="mobOpen = !mobOpen" />

  <main>
    <HeroSection />
    <AboutSection />
    <ProgramsSection />
    <ImpactSection />
    <TeamSection />
    <TestimonialsSection />
    <NewsSection />
    <GallerySection />
    <DonateSection />
    <ContactSection />
  </main>

  <TheFooter />
</template>

<script setup>
import { ref } from 'vue'

import { useReveal } from '../src/composables/useReveal.js'
import TheCursor from '../src//components/TheCursor.vue'
import TheNavbar from '../src/components/TheNavbar.vue'
import HeroSection from '../src/components/HeroSection.vue'
import AboutSection from '../src/components/AboutSection.vue'
import ProgramsSection from '../src/components/ProgramsSection.vue'
import ImpactSection from '../src/components/ImpactSection.vue'
import TeamSection from '../src/components/TeamSection.vue'
import TestimonialsSection from '../src/components/TestimonialsSection.vue'
import NewsSection from '../src/components/NewsSection.vue'
import GallerySection from '../src/components/GallerySection.vue'
import DonateSection from '../src/components/DonateSection.vue'
import ContactSection from '../src/components/ContactSection.vue'
import TheFooter from '../src/components/TheFooter.vue'
const mobOpen = ref(false)

// Boot scroll-reveal after all components mount
useReveal()
</script>
