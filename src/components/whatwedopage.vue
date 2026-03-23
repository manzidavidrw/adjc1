<template>
  <div class="what-we-do-page">

    <!-- ═══ HERO ═══ -->
    <section class="relative bg-navy-dark min-h-[52vh] flex items-end overflow-hidden pt-[104px]">
      <div class="absolute inset-0 bg-hero-mesh"></div>
      <div class="absolute inset-0 grid-lines"></div>
      <div class="absolute left-0 top-[20%] bottom-[20%] w-[3px] bg-red"></div>
      <div
        class="absolute right-0 bottom-0 font-display font-bold text-white/[.025] leading-none select-none pointer-events-none"
        style="font-size: 26vw">05</div>

      <div class="relative max-w-[1280px] mx-auto px-8 pb-16 w-full">
        <!-- Breadcrumb -->
        <div class="flex items-center gap-2 mb-6">
          <button @click="$emit('navigate', 'home')"
            class="text-white/35 font-body text-xs hover:text-white/70 transition-colors bg-transparent border-none cursor-pointer">
            {{ lang === 'fr' ? 'Accueil' : 'Home' }}
          </button>
          <span class="text-white/20 text-xs">›</span>
          <span class="text-red font-body text-xs font-semibold">
            {{ lang === 'fr' ? 'Ce Que Nous Faisons' : 'What We Do' }}
          </span>
        </div>

        <div class="flex items-center gap-3 mb-4">
          <span class="w-8 h-[2px] bg-red flex-shrink-0"></span>
          <span class="text-red font-body text-[.65rem] font-semibold tracking-[3px] uppercase">
            {{ lang === 'fr' ? 'Nos 5 Programmes' : 'Our 5 Programs' }}
          </span>
        </div>

        <h1 class="font-display font-bold text-white leading-[1.06]" style="font-size: clamp(2.8rem, 5vw, 4.5rem)">
          {{ lang === 'fr' ? 'Ce Que Nous ' : 'What We ' }}
          <em class="not-italic text-red">{{ lang === 'fr' ? 'Faisons' : 'Do' }}</em>
        </h1>

        <p class="text-white/50 font-body font-light mt-4 max-w-[640px] leading-[1.85]" style="font-size: .95rem">
          {{ lang === 'fr'
            ? `Cinq programmes intégrés et communautaires pour autonomiser les jeunes congolais et créer un changement
          durable et positif.`
            : `Five integrated, community-based programs to empower Congolese youth and create lasting, positive change.`
          }}
        </p>

        <!-- Program quick-nav pills -->
        <div class="flex flex-wrap gap-3 mt-8">
          <button v-for="(prog, i) in programs" :key="prog.slug" @click="activeProgramIndex = i; scrollToProgram(i)"
            :class="[
              'flex items-center gap-2 px-4 py-2 rounded-full font-body text-xs font-semibold tracking-wide border-none cursor-pointer transition-all duration-200',
              activeProgramIndex === i
                ? 'bg-red text-white'
                : 'bg-white/[.08] text-white/60 hover:bg-white/[.15] hover:text-white border border-white/[.1]'
            ]">
            <span>{{ prog.ico }}</span>
            {{ lang === 'fr' ? prog.shortFr : prog.shortEn }}
          </button>
        </div>
      </div>
    </section>

    <!-- ═══ PROGRAMS — one section per program ═══ -->
    <div v-for="(prog, pi) in programs" :key="prog.slug" :ref="el => progRefs[pi] = el">
      <!-- Program header band -->
      <div :class="['py-16 relative overflow-hidden', pi % 2 === 0 ? 'bg-white' : 'bg-navy-mist']">
        <div class="max-w-[1280px] mx-auto px-8">

          <!-- Program title row -->
          <div class="flex flex-wrap items-center gap-6 mb-12 reveal">
            <div class="w-16 h-16 bg-navy rounded-2xl flex items-center justify-center flex-shrink-0">
              <span class="font-display font-bold text-white text-2xl">0{{ pi + 1 }}</span>
            </div>
            <div>
              <div class="flex items-center gap-3 mb-2">
                <span class="w-6 h-[2px] bg-red flex-shrink-0"></span>
                <span class="text-red font-body text-[.62rem] font-semibold tracking-[3px] uppercase">
                  {{ lang === 'fr' ? 'Programme' : 'Program' }} {{ pi + 1 }}
                </span>
              </div>
              <h2 class="font-display font-bold text-navy leading-[1.1]" style="font-size: clamp(1.8rem, 3vw, 2.6rem)">
                {{ lang === 'fr' ? prog.titleFr : prog.titleEn }}
              </h2>
            </div>
            <div class="ml-auto text-4xl hidden lg:block">{{ prog.ico }}</div>
          </div>

          <!-- Intro: stat card + description -->
          <div class="grid grid-cols-1 lg:grid-cols-[1fr_2fr] gap-12 items-start mb-14">
            <!-- Stat card -->
            <div class="reveal-left">
              <div class="bg-navy rounded-2xl p-8 text-center relative overflow-hidden">
                <div class="absolute top-0 left-0 right-0 h-1 bg-red"></div>
                <div class="text-6xl mb-4">{{ prog.ico }}</div>
                <p class="text-white/40 font-body text-[.62rem] tracking-[2px] uppercase mb-2">
                  {{ lang === 'fr' ? 'Programme' : 'Program' }}
                </p>
                <p class="font-display font-bold text-white text-lg leading-snug">
                  {{ lang === 'fr' ? prog.shortFr : prog.shortEn }}
                </p>
                <div v-if="prog.stat" class="mt-6 pt-5 border-t border-white/[.08]">
                  <div class="font-display font-bold text-red text-3xl">{{ prog.stat }}</div>
                  <div class="text-white/35 font-body text-[.6rem] tracking-[1.5px] uppercase mt-1">
                    {{ lang === 'fr' ? prog.statLabelFr : prog.statLabelEn }}
                  </div>
                </div>
              </div>
            </div>

            <!-- Description + section heading -->
            <div class="reveal-right">
              <p class="text-navy/65 font-body font-light leading-[1.9] text-[.95rem] mb-6">
                {{ lang === 'fr' ? prog.descFr : prog.descEn }}
              </p>
              <div class="flex items-center gap-3">
                <div class="w-8 h-[2px] bg-red"></div>
                <span class="text-navy font-display font-semibold text-lg">
                  {{ lang === 'fr' ? "Domaines Clés d'Intervention" : 'Key Focus Areas' }}
                </span>
              </div>
            </div>
          </div>

          <!-- Sub-program cards — each is a clickable link -->
          <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
            <button v-for="(area, ai) in (lang === 'fr' ? prog.areasFr : prog.areasEn)" :key="area.slug"
              @click="navigateToArea(area.slug)" :class="[
                'reveal text-left bg-white rounded-2xl p-6 border border-navy/[.07]',
                'hover:border-red/40 hover:-translate-y-1 hover:shadow-navy-sm',
                'transition-all duration-300 group cursor-pointer',
                'd' + (ai + 1)
              ]" :aria-label="lang === 'fr' ? `Lire plus sur : ${area.title}` : `Read more about: ${area.title}`">
              <!-- Icon -->
              <div class="flex items-start gap-3">
                <div
                  class="w-9 h-9 rounded-xl bg-red/10 group-hover:bg-red flex items-center justify-center text-base flex-shrink-0 transition-colors duration-300">
                  {{ area.ico }}
                </div>
                <div class="flex-1 min-w-0">
                  <h4 class="font-display font-bold text-navy text-base leading-tight mb-2">
                    {{ area.title }}
                  </h4>
                  <p class="font-body text-navy/55 text-[.78rem] leading-[1.75]">{{ area.desc }}</p>
                </div>
              </div>

              <!-- Read more cue -->
              <div
                class="mt-4 flex items-center gap-1.5 text-red/60 group-hover:text-red transition-colors duration-200">
                <span class="font-body text-[.7rem] font-semibold tracking-wide uppercase">
                  {{ lang === 'fr' ? 'Lire la suite' : 'Read more' }}
                </span>
                <span class="text-sm transition-transform duration-200 group-hover:translate-x-1">→</span>
              </div>
            </button>
          </div>
        </div>
      </div>

      <!-- Gradient divider between programs -->
      <div v-if="pi < programs.length - 1" class="h-[3px] bg-gradient-to-r from-red via-navy to-red"></div>
    </div>

    <!-- ═══ CTA BAND ═══ -->
    <section class="bg-navy py-24 relative overflow-hidden">
      <div class="absolute inset-0 grid-lines opacity-40"></div>
      <div
        class="absolute -right-32 top-1/2 -translate-y-1/2 w-[500px] h-[500px] rounded-full bg-red/[.06] blur-3xl pointer-events-none">
      </div>
      <div class="relative max-w-[1280px] mx-auto px-8 text-center">
        <div class="flex items-center justify-center gap-3 mb-5">
          <span class="w-7 h-[2px] bg-red"></span>
          <span class="text-red font-body text-[.65rem] font-semibold tracking-[3px] uppercase">
            {{ lang === 'fr' ? 'Rejoignez-Nous' : 'Join Us' }}
          </span>
          <span class="w-7 h-[2px] bg-red"></span>
        </div>
        <h2 class="font-display font-bold text-white leading-[1.1] mb-5" style="font-size: clamp(2rem, 3.5vw, 3rem)">
          {{ lang === 'fr' ? 'Soutenez Nos Programmes' : 'Support Our Programs' }}
        </h2>
        <p class="text-white/45 font-body font-light text-sm leading-relaxed max-w-[560px] mx-auto mb-10">
          {{ lang === 'fr'
            ? `Chaque contribution aide un jeune congolais à accéder à l'éducation, à la santé, à la paix et à un avenir
          digne.`
            : `Every contribution helps a Congolese young person access education, health, peace and a dignified future.`
          }}
        </p>
        <div class="flex gap-4 justify-center flex-wrap">
          <button @click="$emit('navigate', 'donate')"
            class="bg-red hover:bg-red-dark text-white font-body font-semibold text-sm px-8 py-4 rounded-xl border-none cursor-pointer transition-all duration-200 hover:-translate-y-0.5 hover:shadow-red-lg">
            {{ lang === 'fr' ? 'Faire un Don' : 'Donate Now' }} →
          </button>
          <button @click="$emit('navigate', 'contact')"
            class="bg-white/[.07] border border-white/[.15] hover:bg-white/[.15] text-white font-body font-semibold text-sm px-8 py-4 rounded-xl cursor-pointer transition-all duration-200">
            {{ lang === 'fr' ? 'Devenir Partenaire' : 'Become a Partner' }}
          </button>
        </div>
      </div>
    </section>

  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { useTranslations } from '../composables/useTranslations.js'
import { useReveal } from '../composables/useReveal.js'
import { programs } from '../data/programData.js'

// ── Props / emits ────────────────────────────────────────────────────────────
const emit = defineEmits(['navigate'])

// ── Composables ───────────────────────────────────────────────────────────────
const { lang } = useTranslations()
useReveal()

// ── Lifecycle ────────────────────────────────────────────────────────────────
onMounted(() => window.scrollTo({ top: 0, behavior: 'smooth' }))

// ── State ────────────────────────────────────────────────────────────────────
const activeProgramIndex = ref(null)
const progRefs = ref([])

// ── Helpers ──────────────────────────────────────────────────────────────────
function scrollToProgram(i) {
  progRefs.value[i]?.scrollIntoView({ behavior: 'smooth', block: 'start' })
}

/**
 * Navigates to the dedicated sub-program article page.
 * Emits 'navigate' with route name 'sub-program' and passes the slug as a
 * parameter so the parent router / App.vue can render SubProgramPage.vue.
 */
function navigateToArea(slug) {
  emit('navigate', 'sub-program', { slug })
}
</script>