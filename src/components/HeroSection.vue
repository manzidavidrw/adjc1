<template>
  <section id="home" class="relative min-h-screen bg-navy-dark flex flex-col justify-end overflow-hidden pt-[108px]">

    <!-- Background layers -->
    <div class="absolute inset-0 bg-hero-mesh"></div>
    <div class="absolute inset-0 grid-lines"></div>

    <!-- Large decorative number -->
    <div
      class="absolute right-0 bottom-0 font-display font-bold leading-none text-white/[.03] select-none pointer-events-none"
      style="font-size:38vw">15</div>

    <!-- Vertical label -->
    <div
      class="hidden lg:block absolute left-6 bottom-36 writing-vertical text-[.55rem] tracking-[4px] uppercase text-white/25 font-body">
      KINSHASA · CONGO · 2010
    </div>

    <!-- Red accent line left -->
    <div class="absolute left-0 top-[25%] bottom-[25%] w-[3px] bg-red"></div>

    <!-- Main content -->
    <div class="relative max-w-[1280px] mx-auto px-8 pb-0 w-full">
      <div class="grid grid-cols-1 lg:grid-cols-[1fr_380px] gap-16 items-end pb-20">

        <!-- Left: text -->
        <div>
          <!-- Eyebrow -->
          <div class="flex items-center gap-3 mb-7 reveal">
            <span class="w-8 h-[2px] bg-red flex-shrink-0"></span>
            <span class="text-red text-[.65rem] font-semibold tracking-[3px] uppercase font-body">{{ t('heroEyebrow')
              }}</span>
          </div>

          <!-- Headline -->
          <h1 class="font-display font-bold text-white leading-[1.04] mb-8 reveal d1"
            style="font-size:clamp(3rem,6vw,5.5rem)">
            {{ beforeItalic }}
            <em class="not-italic text-red">{{ t('heroItalic') }}</em>
            {{ afterItalic }}
          </h1>

          <!-- Sub -->
          <p class="text-white/55 font-body font-light leading-[1.85] max-w-[540px] mb-10 reveal d2"
            style="font-size:clamp(.9rem,1.2vw,1.05rem)">
            {{ t('heroSub') }}
          </p>

          <!-- CTAs -->
          <div class="flex flex-wrap gap-4 reveal d3">
            <button @click="go('programs')"
              class="inline-flex items-center gap-3 bg-red hover:bg-red-dark text-white font-body font-semibold text-sm tracking-wide px-8 py-4 rounded-xl border-none cursor-pointer transition-all duration-300 hover:-translate-y-1 hover:shadow-red-lg">
              {{ t('heroCta1') }}
              <span
                class="w-5 h-5 rounded-full border border-white/40 flex items-center justify-center text-[.6rem]">→</span>
            </button>
            <button @click="go('about')"
              class="inline-flex items-center gap-3 text-white/65 hover:text-white font-body font-medium text-sm tracking-wide px-6 py-4 rounded-xl border border-white/15 hover:border-white/35 bg-transparent cursor-pointer transition-all duration-300">
              {{ t('heroCta2') }}
            </button>
          </div>
        </div>

        <!-- Right: stats card -->
        <div class="hidden lg:block reveal-right">
          <div class="bg-white/[.05] backdrop-blur-xl border border-white/[.08] rounded-2xl overflow-hidden">
            <div class="grid grid-cols-2">
              <div v-for="(stat, i) in stats" :key="i" class="px-6 py-7 text-center border-white/[.07]"
                :class="[i % 2 === 0 ? 'border-r' : '', i < 2 ? 'border-b' : '']">
                <div class="font-display font-bold text-white leading-none mb-1" style="font-size:2.2rem">{{ t(stat.n)
                  }}</div>
                <div class="text-white/35 font-body text-[.6rem] tracking-[1.5px] uppercase">{{ t(stat.l) }}</div>
              </div>
            </div>
            <!-- CTA inside card -->
            <div class="px-6 py-5 border-t border-white/[.07] flex items-center justify-between">
              <span class="text-white/40 text-[.72rem] font-body">{{ t('heroEyebrow') }}</span>
              <span class="w-2 h-2 rounded-full bg-red animate-pulse"></span>
            </div>
          </div>
        </div>
      </div>

      <!-- Bottom ticker -->
      <div class="border-t border-white/[.07] py-4 ticker-track -mx-8">
        <div class="ticker-inner">
          <div v-for="i in 4" :key="i" class="flex items-center">
            <div v-for="tag in t('tickers')" :key="tag + i"
              class="flex items-center gap-3 px-6 text-[.62rem] text-white/30 tracking-[1.5px] uppercase whitespace-nowrap font-body">
              <span class="w-1.5 h-1.5 rounded-full bg-red flex-shrink-0"></span>
              {{ tag }}
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { computed } from 'vue'
import { useTranslations } from '../composables/useTranslations.js'

const { t } = useTranslations()

const stats = [
  { n: 'heroStat1n', l: 'heroStat1l' },
  { n: 'heroStat2n', l: 'heroStat2l' },
  { n: 'heroStat3n', l: 'heroStat3l' },
  { n: 'heroStat4n', l: 'heroStat4l' },
]

const beforeItalic = computed(() => {
  const title = t('heroTitle')
  const italic = t('heroItalic')
  const idx = title.toLowerCase().indexOf(italic.toLowerCase())
  return idx === -1 ? title : title.slice(0, idx)
})
const afterItalic = computed(() => {
  const title = t('heroTitle')
  const italic = t('heroItalic')
  const idx = title.toLowerCase().indexOf(italic.toLowerCase())
  return idx === -1 ? '' : title.slice(idx + italic.length)
})

function go(id) { document.getElementById(id)?.scrollIntoView({ behavior: 'smooth' }) }
</script>
