<template>
  <TheCursor />
  <TheNavbar :mob="mobOpen" :current-page="currentPage" @toggleMob="mobOpen = !mobOpen" @navigate="navigateTo" />

  <!-- ── Sub-pages ── -->
  <WhoWeArePage v-if="currentPage === 'whoweare'" @navigate="navigateTo" />
  <WhatWeDoPage v-else-if="currentPage === 'whatwedo'" @navigate="navigateTo" />

  <!-- ── Home (default) ── -->
  <template v-else>
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
  </template>

  <TheFooter @navigate="navigateTo" />
</template>

<script setup>
import { ref, watch, nextTick } from 'vue'

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
import WhoWeArePage from '../src/components/WhoWeArePage.vue'
import WhatWeDoPage from '../src/components/WhatWeDoPage.vue'

const mobOpen = ref(false)
const currentPage = ref('home')

// Section anchors that live on the home page
const HOME_ANCHORS = new Set(['home', 'about', 'programs', 'impact', 'team', 'news', 'gallery', 'donate', 'contact'])

function navigateTo(target) {
  mobOpen.value = false

  if (target === 'whoweare') {
    currentPage.value = 'whoweare'
    return
  }
  if (target === 'whatwedo') {
    currentPage.value = 'whatwedo'
    return
  }

  // Anything else — go to home first, then scroll
  if (currentPage.value !== 'home') {
    currentPage.value = 'home'
    // Wait for home to render, then scroll to section
    nextTick(() => {
      setTimeout(() => {
        if (HOME_ANCHORS.has(target)) {
          document.getElementById(target)?.scrollIntoView({ behavior: 'smooth' })
        }
      }, 80)
    })
  } else {
    if (HOME_ANCHORS.has(target)) {
      document.getElementById(target)?.scrollIntoView({ behavior: 'smooth' })
    }
  }
}

// Re-run reveal observer whenever page changes
watch(currentPage, () => {
  nextTick(() => useReveal())
})

useReveal()
</script>
