<template>
  <section id="about" class="bg-white py-28">
    <div class="max-w-[1280px] mx-auto px-8">
      <div class="grid grid-cols-1 lg:grid-cols-2 gap-20 items-center">

        <!-- Visual side -->
        <div class="reveal-left relative">
          <!-- Main tall card -->
          <div class="relative aspect-[4/5] rounded-2xl overflow-hidden bg-navy">
            <!-- Background gradient -->
            <div class="absolute inset-0 bg-gradient-to-br from-navy-light to-navy-dark"></div>
            <!-- Grid lines inside -->
            <div class="absolute inset-0 grid-lines opacity-50"></div>
            <!-- Quote content -->
            <div class="absolute inset-0 flex flex-col justify-end p-10">
              <div class="w-10 h-[3px] bg-red mb-6"></div>
              <blockquote class="font-display text-white text-2xl font-semibold leading-[1.35] italic mb-4">
                {{ t('aboutQuote') }}
              </blockquote>
              <cite class="text-white/40 font-body text-xs tracking-[2px] uppercase not-italic">{{ t('aboutQuoteBy')
                }}</cite>
            </div>
          </div>

          <!-- Floating year badge -->
          <div
            class="absolute -top-5 -right-5 w-24 h-24 bg-red rounded-2xl flex flex-col items-center justify-center shadow-red-lg z-10">
            <span class="font-display font-bold text-white text-[2rem] leading-none">15</span>
            <span class="text-white/70 font-body text-[.45rem] tracking-[1px] uppercase text-center leading-tight mt-1"
              style="white-space:pre-line">{{ t('badge') }}</span>
          </div>

          <!-- Small floating card -->
          <div class="absolute -bottom-6 -left-6 bg-navy rounded-2xl px-6 py-5 shadow-navy-lg z-10">
            <div class="text-white/40 font-body text-[.58rem] tracking-[2px] uppercase mb-1">RDC</div>
            <div class="font-display font-bold text-white text-2xl leading-none">12</div>
            <div class="text-white/50 font-body text-[.65rem] mt-1">Provinces couvertes</div>
          </div>
        </div>

        <!-- Text side -->
        <div class="reveal-right">
          <!-- Eyebrow -->
          <div class="flex items-center gap-3 mb-5">
            <span class="w-7 h-[2px] bg-red flex-shrink-0"></span>
            <span class="text-red font-body text-[.65rem] font-semibold tracking-[3px] uppercase">{{ t('aboutEye')
              }}</span>
          </div>

          <h2 class="font-display font-bold text-navy leading-[1.1] mb-7" style="font-size:clamp(2.2rem,3.5vw,3rem)">
            {{ t('aboutTitle') }}
          </h2>

          <p class="text-navy/60 font-body font-light leading-[1.85] mb-5" style="font-size:.95rem">{{ t('aboutP1') }}
          </p>
          <p class="text-navy/60 font-body font-light leading-[1.85] mb-10" style="font-size:.95rem">{{ t('aboutP2') }}
          </p>

          <!-- Mission / Vision cards -->
          <div class="grid grid-cols-2 gap-4">
            <div class="bg-navy rounded-xl p-6 group hover:bg-navy-light transition-colors duration-300">
              <div class="w-8 h-[2px] bg-red mb-4"></div>
              <h4 class="font-display font-bold text-white text-lg mb-2">{{ t('missionTitle') }}</h4>
              <p class="text-white/50 font-body text-xs leading-[1.7]">{{ t('missionText') }}</p>
            </div>
            <div
              class="bg-red-pale border border-red/15 rounded-xl p-6 group hover:border-red/40 transition-colors duration-300">
              <div class="w-8 h-[2px] bg-red mb-4"></div>
              <h4 class="font-display font-bold text-navy text-lg mb-2">{{ t('visionTitle') }}</h4>
              <p class="text-navy/60 font-body text-xs leading-[1.7]">{{ t('visionText') }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { useTranslations } from '../composables/useTranslations.js'
const { t } = useTranslations()
</script>
