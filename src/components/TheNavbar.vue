<template>
  <!-- ═══════════════════════════════════════════════════════
       Single fixed wrapper → lang bar + navbar always together.
       Lang bar collapses smoothly on scroll — no overlap ever.
  ════════════════════════════════════════════════════════════ -->
  <div class="fixed top-0 left-0 right-0 z-[400]" @mouseleave="activeMenu = null">

    <!-- ── Lang / utility bar ── -->
    <div :class="['bg-navy-dark border-b border-white/[.06] flex items-center justify-between px-8 overflow-hidden transition-all duration-500',
      scrolled ? 'h-0 opacity-0 border-b-0' : 'h-9 opacity-100']">
      <!-- Left info -->
      <div class="flex items-center gap-4">
        <span class="text-white/30 font-body text-[.6rem] tracking-[1.5px]">✉ info@adjcongo.org</span>
        <span class="text-white/15">|</span>
        <span class="text-white/30 font-body text-[.6rem] tracking-[1.5px]">☎ +243 81 234 5678</span>
      </div>
      <!-- Right: lang toggle -->
      <div class="flex items-center gap-1">
        <button v-for="l in ['fr', 'en']" :key="l" @click="lang = l" :class="['text-[.62rem] font-semibold tracking-[2px] uppercase px-3 py-0.5 rounded-sm transition-all duration-200 border-none cursor-pointer font-body',
          lang === l ? 'bg-red text-white' : 'bg-transparent text-white/40 hover:text-white/70']">{{ l
          }}</button>
      </div>
    </div>

    <!-- ── Main navbar ── -->
    <nav :class="['transition-all duration-500',
      scrolled ? 'bg-navy-dark/96 backdrop-blur-2xl shadow-[0_4px_30px_rgba(0,0,0,.35)]' : 'bg-transparent']">
      <div class="max-w-[1280px] mx-auto px-8 h-[68px] flex items-center justify-between">

        <!-- Logo -->
        <button @click="navigate('home')"
          class="flex items-center gap-3 bg-transparent border-none cursor-pointer group flex-shrink-0">
          <div
            class="w-10 h-10 bg-red rounded-lg flex items-center justify-center flex-shrink-0 group-hover:bg-red-dark transition-colors duration-200">
            <span class="font-display font-bold text-white text-sm tracking-tight">ADJ</span>
          </div>
          <div class="text-left">
            <div class="font-display font-bold text-white text-lg tracking-[2px] leading-none">ADJC</div>
            <div class="text-[.5rem] text-white/35 tracking-[1.5px] uppercase mt-0.5 font-body">{{ t('logoSub') }}</div>
          </div>
        </button>

        <!-- Desktop mega menu links -->
        <div class="hidden lg:flex items-center h-full">
          <div v-for="menu in menus" :key="menu.key" class="relative h-full flex items-center"
            @mouseenter="activeMenu = menu.key">
            <!-- Top-level label -->
            <button
              class="flex items-center gap-1.5 h-full px-5 text-[.7rem] font-semibold tracking-[1px] uppercase font-body border-none bg-transparent cursor-pointer transition-colors duration-200"
              :class="activeMenu === menu.key ? 'text-white' : 'text-white/60 hover:text-white'">
              {{ t(menu.label) }}
              <!-- Chevron -->
              <svg class="w-3 h-3 transition-transform duration-200"
                :class="activeMenu === menu.key ? 'rotate-180' : ''" fill="none" viewBox="0 0 12 12">
                <path d="M2 4l4 4 4-4" stroke="currentColor" stroke-width="1.5" stroke-linecap="round"
                  stroke-linejoin="round" />
              </svg>
            </button>
            <!-- Active underline bar -->
            <div class="absolute bottom-0 left-5 right-5 h-[2px] bg-red transition-transform duration-200 origin-left"
              :class="activeMenu === menu.key ? 'scale-x-100' : 'scale-x-0'"></div>

            <!-- ── Dropdown panel ── -->
            <div v-show="activeMenu === menu.key" class="absolute top-full left-1/2 -translate-x-1/2 pt-2 w-[520px]"
              style="filter:drop-shadow(0 20px 40px rgba(0,0,0,.4))">
              <div class="bg-white rounded-2xl overflow-hidden">
                <!-- Panel header -->
                <div class="bg-navy px-6 py-4 flex items-center justify-between">
                  <div>
                    <p class="text-white font-display font-bold text-lg leading-none">{{ t(menu.label) }}</p>
                    <p class="text-white/40 font-body text-[.65rem] mt-1">{{ t(menu.desc) }}</p>
                  </div>
                  <div class="w-10 h-10 bg-red/20 rounded-xl flex items-center justify-center text-xl">{{ menu.ico }}
                  </div>
                </div>
                <!-- Sub-items grid -->
                <div class="grid grid-cols-2 gap-px bg-navy/5 p-1">
                  <button v-for="sub in menu.subs" :key="sub.id" @click="navigate(sub.id); activeMenu = null"
                    class="flex items-start gap-3 px-4 py-4 rounded-xl bg-white hover:bg-navy-mist text-left transition-colors duration-150 border-none cursor-pointer group/sub">
                    <span
                      class="w-8 h-8 rounded-lg bg-navy/5 group-hover/sub:bg-red group-hover/sub:text-white flex items-center justify-center text-base flex-shrink-0 transition-all duration-200">
                      {{ sub.ico }}
                    </span>
                    <div>
                      <p class="font-body font-semibold text-navy text-sm leading-tight">{{ t(sub.label) }}</p>
                      <p class="font-body text-navy/45 text-[.68rem] leading-snug mt-0.5">{{ t(sub.desc) }}</p>
                    </div>
                  </button>
                </div>
              </div>
            </div>
          </div>

          <!-- CTA button -->
          <button @click="navigate('donate')"
            class="ml-4 bg-red hover:bg-red-dark text-white text-[.7rem] font-semibold tracking-[1px] uppercase px-5 py-2.5 rounded-lg border-none cursor-pointer transition-all duration-200 hover:-translate-y-px hover:shadow-red-lg font-body flex-shrink-0">{{
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
  </div>

  <!-- ══════════════════════════════════════
       Mobile full-screen menu with accordion
  ═══════════════════════════════════════════ -->
  <div :class="['fixed inset-0 z-[350] bg-navy-dark flex flex-col overflow-y-auto transition-all duration-500 pt-[104px]',
    mob ? 'opacity-100 pointer-events-auto' : 'opacity-0 pointer-events-none']">

    <div class="flex-1 px-6 py-6 flex flex-col gap-1">
      <div v-for="menu in menus" :key="menu.key">
        <!-- Accordion toggle -->
        <button @click="mobActive = mobActive === menu.key ? null : menu.key"
          class="w-full flex items-center justify-between px-4 py-4 rounded-xl bg-transparent hover:bg-white/[.04] border-none cursor-pointer transition-colors duration-200">
          <span class="font-display font-bold text-white text-2xl">{{ t(menu.label) }}</span>
          <svg class="w-5 h-5 text-white/40 transition-transform duration-300"
            :class="mobActive === menu.key ? 'rotate-180' : ''" fill="none" viewBox="0 0 12 12">
            <path d="M2 4l4 4 4-4" stroke="currentColor" stroke-width="1.5" stroke-linecap="round"
              stroke-linejoin="round" />
          </svg>
        </button>

        <!-- Accordion sub-items -->
        <div class="overflow-hidden transition-all duration-400"
          :style="mobActive === menu.key ? 'max-height:600px;opacity:1' : 'max-height:0;opacity:0'">
          <div class="flex flex-col gap-1 px-2 pb-3">
            <button v-for="sub in menu.subs" :key="sub.id"
              @click="navigate(sub.id); $emit('toggleMob'); mobActive = null"
              class="flex items-center gap-3 px-4 py-3 rounded-xl bg-white/[.03] hover:bg-white/[.07] border-none cursor-pointer text-left transition-colors duration-150">
              <span class="w-8 h-8 rounded-lg bg-red/20 flex items-center justify-center text-base flex-shrink-0">{{
                sub.ico }}</span>
              <div>
                <p class="font-body font-semibold text-white text-sm leading-tight">{{ t(sub.label) }}</p>
                <p class="font-body text-white/35 text-[.65rem]">{{ t(sub.desc) }}</p>
              </div>
            </button>
          </div>
        </div>
      </div>
    </div>

    <!-- Mobile CTA -->
    <div class="px-6 py-6 border-t border-white/[.07]">
      <button @click="navigate('donate'); $emit('toggleMob')"
        class="w-full bg-red hover:bg-red-dark text-white font-body font-semibold text-base py-4 rounded-xl border-none cursor-pointer transition-colors duration-200">{{
          t('navDonate') }} →</button>
      <!-- Lang toggle mobile -->
      <div class="flex items-center justify-center gap-2 mt-5">
        <button v-for="l in ['fr', 'en']" :key="l" @click="lang = l" :class="['text-xs font-semibold tracking-[2px] uppercase px-4 py-2 rounded-lg border-none cursor-pointer font-body transition-all duration-200',
          lang === l ? 'bg-red text-white' : 'bg-white/[.06] text-white/40']">{{ l }}</button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted, onUnmounted } from 'vue'
import { useTranslations } from '@/composables/useTranslations.js'

const { lang, t } = useTranslations()
defineProps({ mob: Boolean, currentPage: String })
const emit = defineEmits(['toggleMob', 'navigate'])

const scrolled = ref(false)
const activeMenu = ref(null)
const mobActive = ref(null)

function navigate(id) {
  activeMenu.value = null
  emit('navigate', id)
}

function onScroll() { scrolled.value = window.scrollY > 30 }

onMounted(() => window.addEventListener('scroll', onScroll, { passive: true }))
onUnmounted(() => window.removeEventListener('scroll', onScroll))
const menus = computed(() => [
  {
    key: 'whatwedo',
    label: 'menuWhatWeDo',
    desc: 'menuWhatWeDoDesc',
    ico: '🚀',
    pageTarget: 'whatwedo',
    subs: [
      { id: 'whatwedo', ico: '🩺', label: 'subSRHR', desc: 'subSRHRDesc', page: true },
      { id: 'whatwedo', ico: '💼', label: 'subEnterprise', desc: 'subEnterpriseDesc', page: true },
      { id: 'whatwedo', ico: '☮️', label: 'subPeace', desc: 'subPeaceDesc', page: true },
      { id: 'whatwedo', ico: '🌿', label: 'subClimate', desc: 'subClimateDesc', page: true },
      { id: 'whatwedo', ico: '🔬', label: 'subResearch', desc: 'subResearchDesc', page: true },
      { id: 'programs', ico: '📋', label: 'subAllPrograms', desc: 'subAllProgramsDesc', page: false },
    ],
  },
  {
    key: 'about',
    label: 'menuAboutUs',
    desc: 'menuAboutUsDesc',
    ico: '🌍',
    pageTarget: 'whoweare',
    subs: [
      { id: 'whoweare', ico: '📖', label: 'subOurStory', desc: 'subOurStoryDesc', page: true },
      { id: 'whoweare', ico: '🎯', label: 'subMission', desc: 'subMissionDesc', page: true },
      { id: 'team', ico: '👥', label: 'subTeam', desc: 'subTeamDesc', page: false },
      { id: 'impact', ico: '📊', label: 'subImpact', desc: 'subImpactDesc', page: false },
      { id: 'whoweare', ico: '🤝', label: 'subPartners', desc: 'subPartnersDesc', page: true },
      { id: 'contact', ico: '💼', label: 'subCareers', desc: 'subCareersDesc', page: false },
    ],
  },
  {
    key: 'news',
    label: 'menuBlogsNews',
    desc: 'menuBlogsNewsDesc',
    ico: '📰',
    pageTarget: 'news',
    subs: [
      { id: 'news', ico: '📢', label: 'subLatestNews', desc: 'subLatestNewsDesc', page: false },
      { id: 'news', ico: '✍️', label: 'subBlog', desc: 'subBlogDesc', page: false },
      { id: 'news', ico: '🎬', label: 'subSuccessStories', desc: 'subSuccessDesc', page: false },
      { id: 'gallery', ico: '📸', label: 'subGallery', desc: 'subGalleryDesc', page: false },
      { id: 'news', ico: '🎙️', label: 'subPressMedia', desc: 'subPressDesc', page: false },
      { id: 'news', ico: '📅', label: 'subEvents', desc: 'subEventsDesc', page: false },
    ],
  },
  {
    key: 'takeaction',
    label: 'menuTakeAction',
    desc: 'menuTakeActionDesc',
    ico: '❤️',
    pageTarget: 'donate',
    subs: [
      { id: 'donate', ico: '💳', label: 'subDonate', desc: 'subDonateDesc', page: false },
      { id: 'contact', ico: '🙌', label: 'subVolunteer', desc: 'subVolunteerDesc', page: false },
      { id: 'contact', ico: '🏢', label: 'subPartnerOrg', desc: 'subPartnerOrgDesc', page: false },
      { id: 'contact', ico: '📣', label: 'subAdvocate', desc: 'subAdvocateDesc', page: false },
      { id: 'contact', ico: '🎓', label: 'subMentor', desc: 'subMentorDesc', page: false },
      { id: 'contact', ico: '📬', label: 'subNewsletter', desc: 'subNewsletterDesc', page: false },
    ],
  },
])


onMounted(() => window.addEventListener('scroll', onScroll, { passive: true }))
onUnmounted(() => window.removeEventListener('scroll', onScroll))
</script>