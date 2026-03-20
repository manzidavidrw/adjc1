<template>
  <!-- Lang bar -->
  <div
    class="fixed top-0 left-0 right-0 z-[400] bg-navy-dark border-b border-white/[.06] flex items-center justify-end px-8 h-9">
    <div class="flex items-center gap-1">
      <button v-for="l in ['fr', 'en']" :key="l" @click="lang = l" :class="['text-[.65rem] font-semibold tracking-[2px] uppercase px-3 py-1 rounded-sm transition-all duration-200 border-none cursor-pointer font-body',
        lang === l ? 'bg-red text-white' : 'bg-transparent text-white/40 hover:text-white/80']">{{ l
        }}</button>
    </div>
  </div>

  <!-- Navbar -->
  <nav :class="['fixed left-0 right-0 z-[300] transition-all duration-500',
    scrolled ? 'top-0 bg-navy-dark/95 backdrop-blur-2xl shadow-navy-lg' : 'top-9 bg-transparent']">
    <div class="max-w-[1280px] mx-auto px-8 h-[68px] flex items-center justify-between">

      <!-- Logo -->
      <button @click="go('home')" class="flex items-center gap-3 bg-transparent border-none cursor-pointer group">
        <div
          class="w-10 h-10 bg-red rounded-lg flex items-center justify-center flex-shrink-0 group-hover:bg-red-dark transition-colors duration-200">
          <span class="font-display font-bold text-white text-sm tracking-tight">ADJ</span>
        </div>
        <div class="text-left">
          <div class="font-display font-bold text-white text-lg tracking-[2px] leading-none">ADJC</div>
          <div class="text-[.52rem] text-white/40 tracking-[1.5px] uppercase mt-0.5 font-body">{{ t('logoSub') }}</div>
        </div>
      </button>

      <!-- Desktop links -->
      <div class="hidden lg:flex items-center gap-1">
        <button v-for="link in links" :key="link.id" @click="go(link.id)"
          class="nav-link text-white/65 hover:text-white text-[.7rem] font-medium tracking-[1px] uppercase px-4 h-[68px] flex items-center bg-transparent border-none cursor-pointer transition-colors duration-200 font-body">{{
            t(link.label) }}</button>
        <button @click="go('donate')"
          class="ml-4 bg-red hover:bg-red-dark text-white text-[.7rem] font-semibold tracking-[1px] uppercase px-5 py-2.5 rounded-lg border-none cursor-pointer transition-all duration-200 hover:-translate-y-px hover:shadow-red-lg font-body">{{
            t('navDonate') }}</button>
      </div>

      <!-- Hamburger -->
      <button @click="$emit('toggleMob')"
        class="lg:hidden flex flex-col justify-center gap-[5px] w-8 h-8 bg-transparent border-none cursor-pointer">
        <span class="block w-5 h-[1.5px] bg-white/70 transition-all duration-300"
          :class="mob ? 'rotate-45 translate-y-[6.5px]' : ''"></span>
        <span class="block w-5 h-[1.5px] bg-white/70 transition-all duration-300"
          :class="mob ? 'opacity-0' : ''"></span>
        <span class="block w-5 h-[1.5px] bg-white/70 transition-all duration-300"
          :class="mob ? '-rotate-45 -translate-y-[6.5px]' : ''"></span>
      </button>
    </div>
  </nav>

  <!-- Mobile menu -->
  <div :class="['fixed inset-0 z-[250] bg-navy-dark flex flex-col items-center justify-center gap-2 transition-all duration-500',
    mob ? 'opacity-100 pointer-events-auto' : 'opacity-0 pointer-events-none']">
    <button v-for="link in links" :key="link.id" @click="go(link.id); $emit('toggleMob')"
      class="font-display text-3xl font-semibold text-white/70 hover:text-white py-3 bg-transparent border-none cursor-pointer transition-colors duration-200">{{
        t(link.label) }}</button>
    <button @click="go('donate'); $emit('toggleMob')"
      class="mt-4 bg-red text-white font-display text-2xl font-semibold px-10 py-3 rounded-xl border-none cursor-pointer hover:bg-red-dark transition-colors duration-200">{{
        t('navDonate') }}</button>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { useTranslations } from '../composables/useTranslations.js'

const { lang, t } = useTranslations()
defineProps({ mob: Boolean })
defineEmits(['toggleMob'])

const scrolled = ref(false)
const links = [
  { id: 'about', label: 'navAbout' },
  { id: 'programs', label: 'navPrograms' },
  { id: 'impact', label: 'navImpact' },
  { id: 'team', label: 'navTeam' },
  { id: 'news', label: 'navNews' },
  { id: 'contact', label: 'navContact' },
]

function go(id) { document.getElementById(id)?.scrollIntoView({ behavior: 'smooth' }) }
onMounted(() => window.addEventListener('scroll', () => { scrolled.value = window.scrollY > 30 }))
</script>
