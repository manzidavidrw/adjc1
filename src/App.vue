<template>
  <TheCursor />
  <TheNavbar :mob="mobOpen" :current-page="currentPage" @toggleMob="mobOpen = !mobOpen" @navigate="navigateTo" />

  <!-- ── Sub-pages ── -->
  <WhoWeArePage v-if="currentPage === 'whoweare'" @navigate="navigateTo" />
  <WhatWeDoPage v-else-if="currentPage === 'whatwedo'" @navigate="navigateTo" />
  <SubProgramPage v-else-if="currentPage === 'sub-program'" :slug="currentRouteParams.slug" @navigate="navigateTo" />

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
import { ref, watch, nextTick, onMounted } from 'vue'

import { useReveal } from '../src/composables/useReveal.js'
import TheCursor from '../src/components/TheCursor.vue'
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
import WhoWeArePage from '../src/components/whowearepage.vue'
import WhatWeDoPage from '../src/components/whatwedopage.vue'
import SubProgramPage from '../src/pages/Subprogrampage.vue'

// ── State ─────────────────────────────────────────────────────────────────────
const mobOpen = ref(false)
const currentPage = ref('home')
const currentRouteParams = ref({})

// Section anchors that live on the home page
const HOME_ANCHORS = new Set([
  'home', 'about', 'programs', 'impact',
  'team', 'news', 'gallery', 'donate', 'contact',
])

// ── Navigation ────────────────────────────────────────────────────────────────
/**
 * Central navigation handler used by all components via @navigate.
 *
 * @param {string} target - Route name or home-page anchor id
 * @param {object} params - Optional route params, e.g. { slug: 'srhr-gbv-prevention' }
 */
function navigateTo(target, params = {}) {
  mobOpen.value = false
  currentRouteParams.value = params

  // Named sub-pages
  if (target === 'whoweare') {
    currentPage.value = 'whoweare'
    return
  }
  if (target === 'whatwedo') {
    currentPage.value = 'whatwedo'
    return
  }
  if (target === 'sub-program') {
    currentPage.value = 'sub-program'
    return
  }

  // Home-page section anchors — navigate home first if needed, then scroll
  if (currentPage.value !== 'home') {
    currentPage.value = 'home'
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

// ── Re-run reveal observer on every page change ───────────────────────────────
watch(currentPage, () => nextTick(() => useReveal()))

onMounted(() => useReveal())
</script>