<template>
  <div class="what-we-do-page">

    <!-- ═══ HERO ═══ -->
    <section class="relative bg-navy-dark min-h-[52vh] flex items-end overflow-hidden pt-[104px]">
      <div class="absolute inset-0 bg-hero-mesh"></div>
      <div class="absolute inset-0 grid-lines"></div>
      <div class="absolute left-0 top-[20%] bottom-[20%] w-[3px] bg-red"></div>
      <div
        class="absolute right-0 bottom-0 font-display font-bold text-white/[.025] leading-none select-none pointer-events-none"
        style="font-size:26vw">05</div>

      <div class="relative max-w-[1280px] mx-auto px-8 pb-16 w-full">
        <div class="flex items-center gap-2 mb-6">
          <button @click="$emit('navigate', 'home')"
            class="text-white/35 font-body text-xs hover:text-white/70 transition-colors bg-transparent border-none cursor-pointer">
            {{ lang === 'fr' ? 'Accueil' : 'Home' }}
          </button>
          <span class="text-white/20 text-xs">›</span>
          <span class="text-red font-body text-xs font-semibold">{{ lang === 'fr' ? 'Ce Que Nous Faisons' : 'What We Do'
          }}</span>
        </div>
        <div class="flex items-center gap-3 mb-4">
          <span class="w-8 h-[2px] bg-red flex-shrink-0"></span>
          <span class="text-red font-body text-[.65rem] font-semibold tracking-[3px] uppercase">{{ lang === 'fr' ? `Nos
            5 Programmes` : `Our 5 Programs` }}</span>
        </div>
        <h1 class="font-display font-bold text-white leading-[1.06]" style="font-size:clamp(2.8rem,5vw,4.5rem)">
          {{ lang === 'fr' ? 'Ce Que Nous ' : 'What We ' }}<em class="not-italic text-red">{{ lang === 'fr' ? 'Faisons'
            : 'Do' }}</em>
        </h1>
        <p class="text-white/50 font-body font-light mt-4 max-w-[640px] leading-[1.85]" style="font-size:.95rem">
          {{ lang === 'fr'
            ? `Cinq programmes intégrés et communautaires pour autonomiser les jeunes congolais et créer un changement
          durable et positif.`
            : `Five integrated, community-based programs to empower Congolese youth and create lasting, positive change.`
          }}
        </p>

        <!-- Program pills -->
        <div class="flex flex-wrap gap-3 mt-8">
          <button v-for="(prog, i) in programs" :key="i" @click="activeProgram = i; scrollToProgram(i)"
            :class="['flex items-center gap-2 px-4 py-2 rounded-full font-body text-xs font-semibold tracking-wide border-none cursor-pointer transition-all duration-200',
              activeProgram === i ? 'bg-red text-white' : 'bg-white/[.08] text-white/60 hover:bg-white/[.15] hover:text-white border border-white/[.1]']">
            <span>{{ prog.ico }}</span>
            {{ lang === 'fr' ? prog.shortFr : prog.shortEn }}
          </button>
        </div>
      </div>
    </section>

    <!-- ═══ PROGRAMS — one per section ═══ -->
    <div v-for="(prog, pi) in programs" :key="pi" :ref="el => progRefs[pi] = el">

      <!-- Program header band -->
      <div :class="['py-16 relative overflow-hidden', pi % 2 === 0 ? 'bg-white' : 'bg-navy-mist']">
        <div class="max-w-[1280px] mx-auto px-8">
          <div class="flex flex-wrap items-center gap-6 mb-12 reveal">
            <!-- Number badge -->
            <div class="w-16 h-16 bg-navy rounded-2xl flex items-center justify-center flex-shrink-0">
              <span class="font-display font-bold text-white text-2xl">0{{ pi + 1 }}</span>
            </div>
            <div>
              <div class="flex items-center gap-3 mb-2">
                <span class="w-6 h-[2px] bg-red flex-shrink-0"></span>
                <span class="text-red font-body text-[.62rem] font-semibold tracking-[3px] uppercase">{{ lang === 'fr' ?
                  'Programme' : 'Program' }} {{ pi + 1 }}</span>
              </div>
              <h2 class="font-display font-bold text-navy leading-[1.1]" style="font-size:clamp(1.8rem,3vw,2.6rem)">
                {{ lang === 'fr' ? prog.titleFr : prog.titleEn }}
              </h2>
            </div>
            <div class="ml-auto text-4xl hidden lg:block">{{ prog.ico }}</div>
          </div>

          <!-- Intro paragraph -->
          <div class="grid grid-cols-1 lg:grid-cols-[1fr_2fr] gap-12 items-start mb-14">
            <!-- Left: big icon + mini stats -->
            <div class="reveal-left">
              <div class="bg-navy rounded-2xl p-8 text-center relative overflow-hidden">
                <div class="absolute top-0 left-0 right-0 h-1 bg-red"></div>
                <div class="text-6xl mb-4">{{ prog.ico }}</div>
                <p class="text-white/40 font-body text-[.62rem] tracking-[2px] uppercase mb-2">{{ lang === 'fr' ?
                  'Programme' : 'Program' }}</p>
                <p class="font-display font-bold text-white text-lg leading-snug">{{ lang === 'fr' ? prog.shortFr :
                  prog.shortEn }}</p>
                <div v-if="prog.stat" class="mt-6 pt-5 border-t border-white/[.08]">
                  <div class="font-display font-bold text-red text-3xl">{{ prog.stat }}</div>
                  <div class="text-white/35 font-body text-[.6rem] tracking-[1.5px] uppercase mt-1">{{ lang === 'fr' ?
                    prog.statLabelFr : prog.statLabelEn }}</div>
                </div>
              </div>
            </div>
            <!-- Right: description -->
            <div class="reveal-right">
              <p class="text-navy/65 font-body font-light leading-[1.9] text-[.95rem] mb-6">
                {{ lang === 'fr' ? prog.descFr : prog.descEn }}
              </p>
              <div class="flex items-center gap-3">
                <div class="w-8 h-[2px] bg-red"></div>
                <span class="text-navy font-display font-semibold text-lg">{{ lang === 'fr' ? `Domaines Clés
                  d\'Intervention` : `Key Focus Areas` }}</span>
              </div>
            </div>
          </div>

          <!-- Focus areas grid -->
          <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
            <div v-for="(area, ai) in (lang === 'fr' ? prog.areasFr : prog.areasEn)" :key="ai"
              class="reveal bg-white rounded-2xl p-6 border border-navy/[.07] hover:border-red/30 hover:-translate-y-1 hover:shadow-navy-sm transition-all duration-300 group"
              :class="'d' + (ai + 1)">
              <div class="flex items-start gap-3">
                <div
                  class="w-9 h-9 rounded-xl bg-red/10 group-hover:bg-red flex items-center justify-center text-base flex-shrink-0 transition-colors duration-300">
                  {{ area.ico }}
                </div>
                <div>
                  <h4 class="font-display font-bold text-navy text-base leading-tight mb-2">{{ area.title }}</h4>
                  <p class="font-body text-navy/55 text-[.78rem] leading-[1.75]">{{ area.desc }}</p>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Red divider between programs -->
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
          <span class="text-red font-body text-[.65rem] font-semibold tracking-[3px] uppercase">{{ lang === 'fr' ?
            'Rejoignez-Nous' : 'Join Us' }}</span>
          <span class="w-7 h-[2px] bg-red"></span>
        </div>
        <h2 class="font-display font-bold text-white leading-[1.1] mb-5" style="font-size:clamp(2rem,3.5vw,3rem)">
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
import { useTranslations } from '@/composables/useTranslations.js'
import { useReveal } from '@/composables/useReveal.js'

const { lang } = useTranslations()
defineEmits(['navigate'])

useReveal()
onMounted(() => window.scrollTo({ top: 0, behavior: 'smooth' }))

const activeProgram = ref(null)
const progRefs = ref([])

function scrollToProgram(i) {
  progRefs.value[i]?.scrollIntoView({ behavior: 'smooth', block: 'start' })
}

/* ═══════════════════════════════════════════════════════════
   PROGRAM DATA  — sourced directly from the uploaded document
═══════════════════════════════════════════════════════════ */
const programs = [
  {
    ico: '🩺',
    shortFr: 'Santé Sexuelle & Reproductive',
    shortEn: 'Sexual & Reproductive Health',
    titleFr: 'Santé Sexuelle & Reproductive des Jeunes (SSRD)',
    titleEn: 'Youth Sexual & Reproductive Health and Rights (SRHR)',
    stat: '60%', statLabelFr: 'des bénéficiaires sont des jeunes femmes', statLabelEn: 'of beneficiaries are young women',
    descFr: "Ce programme vise à améliorer la santé, le bien-être et les droits des jeunes — en particulier des adolescentes et des jeunes femmes — grâce à des interventions SSRD globales, adaptées aux jeunes et fondées sur les droits.",
    descEn: "This programme aims to improve the health, wellbeing, and rights of young people — particularly adolescent girls and young women — through comprehensive, youth-friendly and rights-based SRHR interventions.",
    areasFr: [
      { ico: '📚', title: 'Éducation SSRD pour adolescents', desc: "ADJC offre une éducation sur la santé reproductive adaptée à chaque âge, abordant la puberté, le consentement, l'égalité de genre et la prévention des pratiques néfastes." },
      { ico: '🌸', title: 'Hygiène menstruelle (MHM)', desc: "Promotion de la santé menstruelle pour réduire la stigmatisation et favoriser l'accès à des solutions dignes, permettant aux filles de participer pleinement à la vie scolaire." },
      { ico: '🛡️', title: 'Prévention des VBG', desc: "Sensibilisation à la violence basée sur le genre, promotion de l'autonomie corporelle et renforcement des connaissances sur les droits des jeunes filles." },
      { ico: '🔗', title: 'Accès aux services de santé', desc: "Facilitation de l'accès à des informations confidentielles et adaptées, avec orientation vers des services de santé locaux appropriés." },
      { ico: '💪', title: 'Égalité des genres & autonomisation', desc: "Renforcement des compétences et opportunités de leadership des filles et jeunes femmes, tout en engageant les communautés à remettre en question les normes discriminatoires." },
      { ico: '🤲', title: 'Engagement communautaire', desc: "Mobilisation des communautés pour réduire la stigmatisation autour de la SSRD et créer des environnements favorables à l'exercice des droits des jeunes." },
    ],
    areasEn: [
      { ico: '📚', title: 'SRHR Education for Adolescents', desc: "ADJC provides age-appropriate SRHR education covering puberty, reproductive health, consent, gender equality, and prevention of harmful practices." },
      { ico: '🌸', title: 'Menstrual Health Management (MHM)', desc: "Promoting menstrual health and hygiene to reduce stigma and support access to safe, dignified menstrual solutions so girls can fully participate in education." },
      { ico: '🛡️', title: 'Prevention of Gender-Based Violence', desc: "Raising awareness on GBV, promoting bodily autonomy, and strengthening knowledge of rights among young people, particularly girls and young women." },
      { ico: '🔗', title: 'Access to Youth-Friendly Health Services', desc: "Facilitating access to accurate, confidential SRHR information and linking young people to appropriate local health services through referral mechanisms." },
      { ico: '💪', title: 'Gender Equality & Girls\' Empowerment', desc: "Empowering girls with knowledge, skills, and leadership opportunities while engaging communities to challenge discriminatory norms and support equal rights." },
      { ico: '🤲', title: 'Community Engagement', desc: "Mobilizing communities to raise awareness, challenge harmful norms, and reduce stigma so youth can exercise their rights safely and with dignity." },
    ],
  },
  {
    ico: '💼',
    shortFr: 'Entrepreneuriat Jeune',
    shortEn: 'Youth Enterprise',
    titleFr: 'Développement de l\'Entreprise Jeune',
    titleEn: 'Youth Enterprise Development',
    stat: '320+', statLabelFr: 'entreprises créées', statLabelEn: 'businesses created',
    descFr: "Ce programme promeut l'autonomisation économique et l'auto-emploi chez les jeunes en renforçant les compétences entrepreneuriales, l'innovation et l'accès aux opportunités de subsistance.",
    descEn: "This programme promotes economic empowerment and self-reliance among young people by strengthening entrepreneurial skills, innovation, and access to livelihood opportunities.",
    areasFr: [
      { ico: '🎓', title: 'Formation en Entrepreneuriat', desc: "Outille les jeunes avec des compétences pratiques pour créer et gérer des entreprises, incluant la planification, le marketing et la gestion financière." },
      { ico: '💡', title: 'Promotion des Talents & Innovation', desc: "Identifie et nourrit les talents et idées créatives des jeunes, favorisant l'innovation, le leadership et la pensée entrepreneuriale." },
      { ico: '🏪', title: 'Soutien aux Start-ups & Coopératives', desc: "Fournit un soutien technique, financier et opérationnel aux start-ups, micro-entreprises et coopératives dirigées par des jeunes." },
      { ico: '💰', title: 'Littératie Financière', desc: "Développe les connaissances financières des jeunes : budget, épargne et planification pour une stabilité économique à long terme." },
      { ico: '🌐', title: 'Accès aux Marchés & Mentorat', desc: "Met en relation les jeunes avec des marchés, réseaux et mentors pour améliorer la croissance, l'échelle et la durabilité des entreprises." },
      { ico: '🤝', title: 'Participation Économique Inclusive', desc: "Garantit que tous les jeunes, y compris les plus vulnérables, peuvent pleinement participer à l'entrepreneuriat et au développement économique." },
    ],
    areasEn: [
      { ico: '🎓', title: 'Entrepreneurship Training', desc: "Equips young people with practical skills to start and manage businesses: business planning, marketing, financial management, and problem-solving." },
      { ico: '💡', title: 'Youth Talent & Innovation', desc: "Identifies and nurtures young people's talents and creative ideas, fostering innovation, leadership, and entrepreneurial thinking." },
      { ico: '🏪', title: 'Start-up & Cooperative Support', desc: "Provides technical, financial, and operational support to youth-led start-ups, micro-enterprises, and cooperatives for sustainable growth." },
      { ico: '💰', title: 'Financial Literacy', desc: "Builds financial knowledge and money management skills among young people: budgeting, saving, and planning for long-term economic stability." },
      { ico: '🌐', title: 'Market Linkages & Mentorship', desc: "Connects youth with markets, networks, and mentors to enhance business growth, scalability, and sustainability." },
      { ico: '🤝', title: 'Inclusive Economic Participation', desc: "Ensures all young people, including marginalized and vulnerable youth, can fully participate in entrepreneurship and economic development activities." },
    ],
  },
  {
    ico: '☮️',
    shortFr: 'Paix & Sécurité',
    shortEn: 'Peace & Security',
    titleFr: 'Jeunes, Paix et Sécurité',
    titleEn: 'Youth, Peace and Security',
    stat: 'SCR 2250', statLabelFr: 'Agenda ONU YPS', statLabelEn: 'UN YPS Agenda',
    descFr: "Ce programme soutient les jeunes comme acteurs clés de la consolidation de la paix, de la prévention des conflits et de la cohésion sociale, conformément à l'Agenda ONU Jeunes, Paix et Sécurité (SCR 2250).",
    descEn: "This programme supports young people as key actors in peacebuilding, conflict prevention, and social cohesion, in line with the UN Youth, Peace and Security (YPS) Agenda (SCR 2250).",
    areasFr: [
      { ico: '🗳️', title: 'Participation aux Processus de Paix', desc: "Permet aux jeunes de s'engager activement dans les structures communautaires et de gouvernance, contribuant à la prise de décision locale et aux initiatives de paix." },
      { ico: '💬', title: 'Prévention des Conflits & Dialogue', desc: "Outille les jeunes pour prévenir les conflits, arbitrer les différends et communiquer pacifiquement, favorisant l'harmonie dans leurs communautés." },
      { ico: '📜', title: 'Éducation Civique & Justice Sociale', desc: "Sensibilise les jeunes à leurs droits et responsabilités, encourage l'engagement civique actif et la compréhension de la justice sociale." },
      { ico: '🛡️', title: 'Prévention de l\'Extrémisme Violent', desc: "Permet aux jeunes d'identifier et de contrer les risques de radicalisation en menant des initiatives communautaires qui promeuvent la sécurité et la résilience." },
      { ico: '🌍', title: 'Cohésion Sociale & Gouvernance Inclusive', desc: "Encourage les jeunes à bâtir des ponts entre les communautés, à participer à une gouvernance inclusive et à renforcer la confiance dans les systèmes locaux." },
      { ico: '🌟', title: 'Leadership Jeune pour la Réconciliation', desc: "Soutient des projets menés par des jeunes qui promeuvent la réconciliation, la consolidation de la paix et la résilience communautaire." },
    ],
    areasEn: [
      { ico: '🗳️', title: 'Youth Participation in Peacebuilding', desc: "Empowers young people to actively engage in community and governance structures, contributing to local decision-making and peace initiatives." },
      { ico: '💬', title: 'Conflict Prevention & Dialogue', desc: "Equips youth with skills to prevent conflicts, mediate disputes, and communicate peacefully, promoting harmony within their communities." },
      { ico: '📜', title: 'Civic Education & Social Justice', desc: "Raises youth awareness of their rights and responsibilities, fosters understanding of social justice, and encourages active civic engagement." },
      { ico: '🛡️', title: 'Prevention of Violent Extremism', desc: "Enables young people to identify and counter risks of radicalization by leading community-based initiatives that promote safety and resilience." },
      { ico: '🌍', title: 'Social Cohesion & Inclusive Governance', desc: "Encourages youth to build bridges across communities, participate in inclusive governance, and strengthen trust and cooperation in local systems." },
      { ico: '🌟', title: 'Youth Leadership for Reconciliation', desc: "Supports youth-led projects that promote reconciliation, peacebuilding, and community resilience, developing leadership skills and accountability." },
    ],
  },
  {
    ico: '🌿',
    shortFr: 'Résilience Climatique',
    shortEn: 'Climate Resilience',
    titleFr: 'Jeunes & Résilience Climatique',
    titleEn: 'Youth and Climate Resilience',
    stat: '6', statLabelFr: 'axes d\'intervention', statLabelEn: 'intervention axes',
    descFr: "Ce programme renforce la capacité des jeunes et des communautés à répondre aux défis climatiques et environnementaux à travers des actions climatiques menées par les jeunes et des pratiques durables.",
    descEn: "This programme strengthens the capacity of young people and communities to respond to climate change and environmental challenges through youth-led climate action and sustainable practices.",
    areasFr: [
      { ico: '📖', title: 'Sensibilisation & Éducation Climatique', desc: "Éduque les jeunes sur le changement climatique, les défis environnementaux et les pratiques durables, les outillant pour agir dans leurs communautés." },
      { ico: '🌱', title: 'Initiatives d\'Adaptation Climatique', desc: "Soutient les jeunes dans la conception et la mise en œuvre de projets qui aident les communautés à s'adapter aux impacts climatiques et à réduire leur vulnérabilité." },
      { ico: '🌳', title: 'Gestion Durable des Ressources Naturelles', desc: "Engage les jeunes dans la gestion responsable des forêts, de l'eau et des terres, assurant une utilisation durable pour les générations présentes et futures." },
      { ico: '⚡', title: 'Compétences Vertes & Moyens de Subsistance', desc: "Formation aux compétences durables : énergies renouvelables, agriculture intelligente face au climat et entrepreneuriat éco-responsable." },
      { ico: '🌲', title: 'Protection Environnementale & Reboisement', desc: "Mobilise les jeunes pour mener des initiatives de reboisement, de plantation d'arbres et de conservation locale, restaurant les écosystèmes." },
      { ico: '📣', title: 'Plaidoyer Climatique Jeune', desc: "Encourage les jeunes à participer aux campagnes de plaidoyer et aux dialogues politiques sur les questions climatiques, amplificant les voix des jeunes dans la prise de décision." },
    ],
    areasEn: [
      { ico: '📖', title: 'Climate Awareness & Education', desc: "Educates young people on climate change, environmental challenges, and sustainable practices, empowering them to take action in their communities." },
      { ico: '🌱', title: 'Youth-Led Climate Adaptation', desc: "Supports youth to design and implement projects that help communities adapt to climate impacts and reduce vulnerability to climate risks." },
      { ico: '🌳', title: 'Sustainable Natural Resource Management', desc: "Engages young people in responsible management of forests, water, and land for sustainable use by current and future generations." },
      { ico: '⚡', title: 'Green Skills & Climate-Smart Livelihoods', desc: "Training in renewable energy, climate-smart agriculture, and eco-friendly entrepreneurship to boost youth employability and local development." },
      { ico: '🌲', title: 'Environmental Protection & Reforestation', desc: "Empowers youth to lead reforestation, tree planting, and local conservation initiatives, restoring ecosystems and improving community wellbeing." },
      { ico: '📣', title: 'Youth Climate Advocacy', desc: "Encourages young people to participate in advocacy campaigns and policy dialogues on climate issues, amplifying youth voices in decision-making." },
    ],
  },
  {
    ico: '🔬',
    shortFr: 'Recherche & Plaidoyer',
    shortEn: 'Research & Advocacy',
    titleFr: 'Recherche et Plaidoyer',
    titleEn: 'Research and Advocacy',
    stat: 'UPG', statLabelFr: 'Modèle de référence', statLabelEn: 'Reference model',
    descFr: "Chez ADJC, le plaidoyer fondé sur des données probantes est un pilier de notre stratégie de changement systémique. Ce programme renforce les voix des jeunes à la base grâce à la recherche rigoureuse, l'apprentissage participatif et le plaidoyer, ancrés dans notre modèle UPG.",
    descEn: "At ADJC, evidence-based advocacy is a cornerstone of our strategy for systemic change. This programme strengthens grassroots youth voices through rigorous research, participatory learning, and advocacy, rooted in our UPG model and community-based work.",
    areasFr: [
      { ico: '🔎', title: 'Recherche Participative', desc: "Implique les jeunes dans la collecte et l'analyse de données, garantissant que leurs perspectives informent les politiques et les programmes." },
      { ico: '📊', title: 'Plaidoyer Fondé sur les Preuves', desc: "Utilise les résultats de la recherche pour informer les campagnes de plaidoyer, influencer les politiques et promouvoir un changement systémique aux niveaux local et national." },
      { ico: '🎓', title: 'Apprentissage & Partage des Connaissances', desc: "Facilite des ateliers, formations et échanges pour traduire la recherche en solutions concrètes et renforcer les capacités des jeunes." },
      { ico: '📋', title: 'Suivi & Évaluation Communautaires', desc: "Soutient les jeunes dans le suivi des résultats des programmes et de l'impact communautaire, assurant responsabilité et amélioration continue." },
      { ico: '💡', title: 'Changement Transformateur par la Recherche', desc: "Promeut des solutions innovantes et fondées sur la recherche pour les défis auxquels font face les jeunes, les femmes et les communautés." },
      { ico: '🗣️', title: 'Amplification des Voix des Jeunes', desc: "Renforce la capacité des jeunes à articuler leurs besoins et à influencer les décisions qui affectent leur vie au niveau communautaire et politique." },
    ],
    areasEn: [
      { ico: '🔎', title: 'Participatory Youth Research', desc: "Engages young people in data collection and analysis, ensuring their perspectives inform policies and programmes." },
      { ico: '📊', title: 'Evidence-Based Advocacy', desc: "Uses research findings to inform advocacy campaigns, influence policy, and promote systemic change at local and national levels." },
      { ico: '🎓', title: 'Learning & Knowledge Sharing', desc: "Facilitates workshops, training, and exchanges to translate research into actionable solutions and strengthen youth capacity." },
      { ico: '📋', title: 'Community-Based Monitoring & Evaluation', desc: "Supports youth in tracking programme outcomes and community impact, ensuring accountability and continuous improvement." },
      { ico: '💡', title: 'Transformative Change Through Research', desc: "Promotes innovative, research-driven solutions to challenges faced by youth, women, and communities." },
      { ico: '🗣️', title: 'Amplifying Youth Voices', desc: "Strengthens the capacity of young people to articulate their needs and influence decisions that affect their lives at community and policy levels." },
    ],
  },
]
</script>