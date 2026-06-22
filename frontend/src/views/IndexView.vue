<template>
  <div class="index-page min-h-screen bg-primary-50 dark:bg-dark-950">
    <LandingNav />

    <!-- Hero Section -->
    <section class="relative overflow-hidden bg-primary-50 dark:bg-dark-950">
      <div class="mx-auto max-w-7xl px-6 py-12 md:px-8 md:py-24">
        <div class="grid items-center gap-16 lg:grid-cols-2">
          <!-- Left -->
          <div>
            <div class="inline-flex rounded-full bg-primary-100 px-6 py-3 text-sm font-semibold uppercase tracking-wider text-primary-700">
              {{ t('index.hero.badge') }}
            </div>
            <h1 class="mt-10 text-5xl font-bold leading-[1.05] tracking-tight text-gray-900 dark:text-white md:text-[64px]">
              {{ t('index.hero.title') }}<br />
              <span class="text-primary-700">{{ t('index.hero.titleHighlight') }}</span>
            </h1>
            <p class="mt-8 max-w-xl text-lg leading-[1.7] text-gray-500 dark:text-dark-300 md:text-[22px]">
              {{ t('index.hero.description') }}
            </p>
            <div class="mt-8 flex gap-3 md:mt-12 md:gap-5">
              <router-link
                :to="isAuthenticated ? dashboardPath : '/login'"
                class="group flex items-center gap-2 rounded-xl bg-primary-700 px-6 py-3 text-base font-semibold text-white transition hover:bg-primary-800 hover:scale-[1.02] md:gap-3 md:rounded-2xl md:px-12 md:py-5 md:text-xl"
              >
                {{ t('index.hero.enterConsole') }}
                <svg class="h-5 w-5 transition group-hover:translate-x-1 md:h-6 md:w-6" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" d="M5 12h14m-6-6 6 6-6 6" />
                </svg>
              </router-link>
              <a href="/model-pricing" class="rounded-xl border border-gray-200 bg-white px-6 py-3 text-base font-semibold text-gray-800 transition hover:border-primary-300 dark:border-dark-700 dark:bg-dark-900 dark:text-white md:rounded-2xl md:px-12 md:py-5 md:text-xl">
                {{ t('index.hero.viewPricing') }}
              </a>
            </div>
          </div>

          <!-- Right: SVG Hero Illustration -->
          <div class="relative hidden lg:flex items-center justify-center" style="min-height: 480px;">
            <svg viewBox="0 0 600 600" class="h-full w-full" fill="none" xmlns="http://www.w3.org/2000/svg">
              <!-- Dashed connection lines -->
              <line x1="300" y1="300" x2="160" y2="145" stroke="#b3c8ff" stroke-width="2" stroke-dasharray="8 6" />
              <line x1="300" y1="300" x2="470" y2="120" stroke="#b3c8ff" stroke-width="2" stroke-dasharray="8 6" />
              <line x1="300" y1="300" x2="170" y2="460" stroke="#b3c8ff" stroke-width="2" stroke-dasharray="8 6" />
              <line x1="300" y1="300" x2="480" y2="430" stroke="#b3c8ff" stroke-width="2" stroke-dasharray="8 6" />

              <!-- Center dashed orbit circle -->
              <circle cx="300" cy="300" r="130" stroke="#85a3ff" stroke-width="1.5" stroke-dasharray="6 6" fill="none" />

              <!-- Center TOKEN card -->
              <rect x="240" y="240" width="120" height="120" rx="28" fill="#0000ff" />
              <rect x="268" y="270" width="64" height="8" rx="4" fill="white" opacity="0.9" />
              <rect x="268" y="288" width="48" height="8" rx="4" fill="white" opacity="0.6" />
              <rect x="268" y="306" width="56" height="8" rx="4" fill="white" opacity="0.4" />

              <!-- Claude circle -->
              <circle cx="160" cy="145" r="60" fill="white" stroke="#b3c8ff" stroke-width="2" />
              <text x="160" y="138" text-anchor="middle" font-size="28" font-weight="bold" fill="#0000ff" font-family="system-ui, sans-serif">A\</text>
              <text x="160" y="168" text-anchor="middle" font-size="16" font-weight="500" fill="#0609cd" font-family="system-ui, sans-serif">Claude</text>

              <!-- All Models circle -->
              <circle cx="470" cy="120" r="56" fill="white" stroke="#b3c8ff" stroke-width="2" />
              <path d="M455 108l15-10 15 10-15 10z M452 116l18 10 18-10v8l-18 10-18-10z" fill="#0000ff" />
              <text x="470" y="150" text-anchor="middle" font-size="12" font-weight="500" fill="#0609cd" font-family="system-ui, sans-serif">All Models</text>

              <!-- ChatGPT circle -->
              <circle cx="170" cy="460" r="56" fill="white" stroke="#b3c8ff" stroke-width="2" />
              <g transform="translate(148, 432)">
                <path d="M22 12a9.7 9.7 0 0 0-.8-3.9c-1.1-2.2-3.2-3.6-5.5-3.9a7.5 7.5 0 0 0-5.2 1.3A7.3 7.3 0 0 0 7.8 9a7.5 7.5 0 0 0-3.7 2.7A7.3 7.3 0 0 0 3 16a9.7 9.7 0 0 0 .8 3.9c1.1 2.2 3.2 3.6 5.5 3.9a7.5 7.5 0 0 0 5.2-1.3 7.3 7.3 0 0 0 2.7-3.5 7.5 7.5 0 0 0 3.7-2.7A7.3 7.3 0 0 0 22 12z" stroke="#0000ff" stroke-width="1.5" fill="none" />
              </g>
              <text x="170" y="484" text-anchor="middle" font-size="14" font-weight="500" fill="#0609cd" font-family="system-ui, sans-serif">ChatGPT</text>

              <!-- Gemini circle -->
              <circle cx="480" cy="430" r="48" fill="white" stroke="#b3c8ff" stroke-width="2" />
              <path d="M480 406l4 16 16 4-16 4-4 16-4-16-16-4 16-4z" fill="#0000ff" />
              <text x="480" y="454" text-anchor="middle" font-size="13" font-weight="500" fill="#0609cd" font-family="system-ui, sans-serif">Gemini</text>
            </svg>
          </div>
        </div>
      </div>
    </section>


    <!-- Supported Tools Section -->
    <section class="px-6 py-10 md:py-20 bg-primary-100 dark:bg-dark-900">
      <div class="mx-auto max-w-6xl">
        <p class="mb-3 text-sm font-semibold text-primary-600">{{ t('index.tools.subtitle') }}</p>
        <h2 class="mb-12 text-3xl font-bold text-gray-900 md:text-3xl">{{ t('index.tools.title') }}</h2>
        <div class="grid grid-cols-1 gap-6 sm:grid-cols-2 lg:grid-cols-4">
          <div v-for="tool in tools" :key="tool.name" class="group flex flex-col justify-between rounded-2xl bg-white p-7 shadow-sm transition-all hover:shadow-lg dark:bg-dark-900 dark:border dark:border-dark-700">
            <div>
              <div class="mb-6 flex h-14 w-14 items-center justify-center rounded-xl bg-primary-50">
                <Icon :name="tool.icon" size="lg" class="text-primary-600" />
              </div>
              <h3 class="mb-3 text-xl font-bold text-gray-900 dark:text-white">{{ tool.name }}</h3>
              <p class="mb-6 text-sm leading-relaxed text-gray-500 dark:text-dark-300">{{ tool.desc }}</p>
            </div>
            <p class="text-xs font-semibold tracking-wide text-primary-600">{{ tool.tag }}</p>
          </div>
        </div>
      </div>
    </section>

    <!-- Pricing Section -->
    <section id="pricing" class="px-6 py-10 md:py-20">
      <div class="mx-auto max-w-6xl">
        <p class="mb-3 text-center text-sm font-semibold text-primary-600">{{ t('index.pricing.subtitle') }}</p>
        <h2 class="mb-4 text-center text-3xl font-bold text-gray-900 dark:text-white md:text-4xl">{{ t('index.pricing.title') }}</h2>
        <p class="mb-14 text-center text-base text-gray-500 dark:text-dark-300">{{ t('index.pricing.description') }}</p>
        <div class="grid gap-6 md:grid-cols-3">
          <!-- PAYGO Card -->
          <div class="flex flex-col justify-between rounded-2xl border border-gray-200 bg-white p-8 transition-all hover:shadow-lg dark:border-dark-700 dark:bg-dark-900">
            <div>
              <p class="mb-4 text-sm font-bold tracking-widest text-gray-900 dark:text-white">{{ t('index.pricing.paygo.name') }}</p>
              <h3 class="mb-1 text-2xl font-bold text-gray-900">{{ t('index.pricing.paygo.title') }}</h3>
              <p class="mb-8 text-sm text-gray-500">{{ t('index.pricing.paygo.subtitle') }}</p>
              <ul class="mb-8 space-y-4">
                <li class="flex items-start gap-2 text-sm text-gray-600">
                  <Icon name="check" size="sm" class="mt-0.5 text-primary-500" />
                  <span>{{ t('index.pricing.paygo.feature1') }}</span>
                </li>
                <li class="flex items-start gap-2 text-sm text-gray-600">
                  <Icon name="check" size="sm" class="mt-0.5 text-primary-500" />
                  <span>{{ t('index.pricing.paygo.feature2') }}</span>
                </li>
                <li class="flex items-start gap-2 text-sm text-primary-600 font-semibold">
                  <Icon name="check" size="sm" class="mt-0.5 text-primary-500" />
                  <span>{{ t('index.pricing.paygo.feature3') }}</span>
                </li>
              </ul>
            </div>
            <router-link :to="isAuthenticated ? '/purchase' : '/login'" class="block w-full rounded-xl bg-gray-900 py-3.5 text-center text-sm font-medium text-white transition-colors hover:bg-black">
              {{ t('index.pricing.paygo.cta') }}
            </router-link>
          </div>

          <!-- Claude Card -->
          <div class="relative flex flex-col justify-between rounded-2xl border-2 border-primary-300 bg-white p-8 transition-all hover:shadow-lg dark:bg-dark-900">
            <div class="absolute -top-3.5 left-1/2 -translate-x-1/2">
              <span class="rounded-full bg-primary-600 px-4 py-1 text-xs font-semibold text-white">{{ t('index.pricing.claude.recommended') }}</span>
            </div>
            <div>
              <div class="mb-4 flex items-center gap-2">
                <span class="text-base font-bold text-gray-900 dark:text-white">A\</span>
                <span class="text-base font-bold text-gray-900 dark:text-white">{{ t('index.pricing.claude.title') }}</span>
              </div>
              <div class="mb-2">
                <span class="text-3xl font-bold text-gray-900 dark:text-white">{{ t('index.pricing.claude.ratio') }}</span>
                <span class="ml-2 text-lg font-semibold text-gray-900 dark:text-white">{{ t('index.pricing.claude.ratioLabel') }}</span>
              </div>
              <p class="mb-6 text-sm text-gray-500 dark:text-dark-300">{{ t('index.pricing.claude.description') }}</p>
              <ul class="mb-8 space-y-4">
                <li class="flex items-start gap-2 text-sm text-gray-600">
                  <Icon name="check" size="sm" class="mt-0.5 text-primary-500" />
                  <span>{{ t('index.pricing.claude.feature1') }}</span>
                </li>
                <li class="flex items-start gap-2 text-sm text-gray-600">
                  <Icon name="check" size="sm" class="mt-0.5 text-primary-500" />
                  <span>{{ t('index.pricing.claude.feature2') }}</span>
                </li>
                <li class="flex items-start gap-2 text-sm text-gray-600">
                  <Icon name="check" size="sm" class="mt-0.5 text-primary-500" />
                  <span>{{ t('index.pricing.claude.feature3') }}</span>
                </li>
              </ul>
            </div>
            <router-link :to="isAuthenticated ? '/purchase' : '/login'" class="block w-full rounded-xl bg-primary-600 py-3.5 text-center text-sm font-medium text-white transition-colors hover:bg-primary-700">
              {{ t('index.pricing.claude.cta') }}
            </router-link>
          </div>

          <!-- ChatGPT Card -->
          <div class="relative flex flex-col justify-between rounded-2xl border-2 border-primary-300 bg-white p-8 transition-all hover:shadow-lg dark:bg-dark-900">
            <div class="absolute -top-3.5 left-1/2 -translate-x-1/2">
              <span class="rounded-full bg-primary-600 px-4 py-1 text-xs font-semibold text-white">{{ t('index.pricing.chatgpt.recommended') }}</span>
            </div>
            <div>
              <div class="mb-4 flex items-center gap-2">
                <Icon name="auto_awesome" size="lg" class="text-gray-900 dark:text-white" />
                <span class="text-base font-bold text-gray-900 dark:text-white">{{ t('index.pricing.chatgpt.title') }}</span>
              </div>
              <div class="mb-2">
                <span class="text-3xl font-bold text-gray-900 dark:text-white">{{ t('index.pricing.chatgpt.ratio') }}</span>
                <span class="ml-2 text-lg font-semibold text-gray-900 dark:text-white">{{ t('index.pricing.chatgpt.ratioLabel') }}</span>
              </div>
              <p class="mb-6 text-sm text-gray-500 dark:text-dark-300">{{ t('index.pricing.chatgpt.description') }}</p>
              <ul class="mb-8 space-y-4">
                <li class="flex items-start gap-2 text-sm text-gray-600">
                  <Icon name="check" size="sm" class="mt-0.5 text-primary-500" />
                  <span>{{ t('index.pricing.chatgpt.feature1') }}</span>
                </li>
                <li class="flex items-start gap-2 text-sm text-gray-600">
                  <Icon name="check" size="sm" class="mt-0.5 text-primary-500" />
                  <span>{{ t('index.pricing.chatgpt.feature2') }}</span>
                </li>
                <li class="flex items-start gap-2 text-sm text-gray-600">
                  <Icon name="check" size="sm" class="mt-0.5 text-primary-500" />
                  <span>{{ t('index.pricing.chatgpt.feature3') }}</span>
                </li>
              </ul>
            </div>
            <router-link :to="isAuthenticated ? '/purchase' : '/login'" class="block w-full rounded-xl bg-primary-600 py-3.5 text-center text-sm font-medium text-white transition-colors hover:bg-primary-700">
              {{ t('index.pricing.chatgpt.cta') }}
            </router-link>
          </div>
        </div>
      </div>
    </section>

    <!-- Features Section -->
    <section class="px-6 py-10 md:py-20 bg-primary-100 dark:bg-dark-900">
      <div class="mx-auto max-w-5xl">
        <h2 class="mb-4 text-center text-2xl font-bold text-gray-900 dark:text-white md:text-3xl">{{ t('index.features.title') }}</h2>
        <p class="mb-12 text-center text-sm text-gray-500 dark:text-dark-300">{{ t('index.features.subtitle') }}</p>
        <div class="grid gap-6 md:grid-cols-2">
          <div v-for="feature in features" :key="feature.title" class="rounded-2xl border border-gray-100 bg-white p-6 transition-all hover:shadow-md dark:border-dark-700 dark:bg-dark-900">
            <div class="mb-4 flex h-10 w-10 items-center justify-center rounded-lg bg-primary-50">
              <Icon :name="feature.icon" size="md" class="text-primary-600" />
            </div>
            <h3 class="mb-2 text-base font-semibold text-gray-900">{{ feature.title }}</h3>
            <p class="text-sm leading-relaxed text-gray-500">{{ feature.desc }}</p>
          </div>
        </div>
      </div>
    </section>

    <!-- FAQ Section -->
    <section id="faq" class="px-6 py-10 md:py-20">
      <div class="mx-auto max-w-3xl">
        <h2 class="mb-12 text-center text-2xl font-bold text-gray-900 dark:text-white md:text-3xl">{{ t('index.faq.title') }}</h2>
        <div class="space-y-4">
          <div v-for="(faq, idx) in faqs" :key="idx" class="rounded-xl border border-primary-100 bg-primary-100 dark:border-dark-700 dark:bg-dark-900">
            <button
              class="flex w-full items-center justify-between px-6 py-5 text-left"
              @click="toggleFaq(idx)"
            >
              <span class="pr-4 text-sm font-semibold text-gray-900 dark:text-white">{{ faq.q }}</span>
              <span
                class="shrink-0 text-[20px] text-primary-500 transition-transform duration-200"
                :class="{ 'rotate-180': openFaq === idx }"
              >
                <Icon name="expand_more" size="md" class="inline-flex" />
              </span>
            </button>
            <div v-show="openFaq === idx" class="border-t border-primary-100 px-6 pb-5 pt-4">
              <p class="text-sm leading-relaxed text-gray-500 dark:text-dark-300">{{ faq.a }}</p>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Bottom CTA -->
    <section class="px-6 py-10 md:py-20 bg-primary-100 dark:bg-dark-900">
      <div class="mx-auto max-w-3xl rounded-2xl border border-primary-100 bg-gradient-to-br from-primary-50 to-primary-100/50 p-8 text-center md:p-12 dark:border-dark-700 dark:from-dark-900 dark:to-dark-950">
        <h2 class="mb-4 text-2xl font-bold text-gray-900 dark:text-white md:text-3xl">{{ t('index.cta.title') }}</h2>
        <p class="mb-8 text-sm leading-relaxed text-gray-500 dark:text-dark-300">
          {{ t('index.cta.description') }}
        </p>
        <router-link
          :to="isAuthenticated ? dashboardPath : '/register'"
          class="inline-flex items-center gap-2 rounded-full bg-primary-700 px-8 py-3 text-sm font-medium text-white shadow-lg shadow-primary-700/20 transition-all hover:bg-primary-800"
        >
          {{ isAuthenticated ? t('index.cta.enterConsole') : t('index.cta.freeRegister') }}
          <Icon name="arrow_forward" size="sm" class="inline-flex" />
        </router-link>
      </div>
    </section>

    <!-- Footer -->
    <footer class="border-t border-gray-200/60 px-6 py-8">
      <div class="mx-auto flex max-w-6xl flex-col items-center justify-between gap-4 sm:flex-row">
        <div class="flex items-center gap-2">
          <div class="h-6 w-6 overflow-hidden rounded-md">
            <img :src="siteLogo || '/logo.svg'" alt="Logo" class="h-full w-full object-contain" />
          </div>
          <span class="text-sm font-semibold text-primary-800">{{ siteName }}</span>
        </div>
        <p class="text-xs text-gray-400">&copy; {{ currentYear }} {{ siteName }}. {{ t('index.footer.allRightsReserved') }}</p>
      </div>
    </footer>
  </div>
</template>

<script setup lang="ts">
import { ref, computed, onMounted } from 'vue'
import { useI18n } from 'vue-i18n'
import { useAuthStore, useAppStore } from '@/stores'
import LandingNav from '@/components/layout/LandingNav.vue'
import Icon from '@/components/icons/Icon.vue'
import type { IconName } from '@/components/icons/Icon.vue'

const { t } = useI18n()

const authStore = useAuthStore()
const appStore = useAppStore()

const siteName = computed(() => appStore.cachedPublicSettings?.site_name || appStore.siteName || 'pineai.net')
const siteLogo = computed(() => appStore.cachedPublicSettings?.site_logo || appStore.siteLogo || '')

const isAuthenticated = computed(() => authStore.isAuthenticated)
const isAdmin = computed(() => authStore.isAdmin)
const dashboardPath = computed(() => isAdmin.value ? '/admin/dashboard' : '/dashboard')
const currentYear = computed(() => new Date().getFullYear())

const tools = computed<Array<{ name: string; icon: IconName; desc: string; tag: string }>>(() => [
  {
    name: t('index.tools.openclaw.name'),
    icon: 'auto_awesome',
    desc: t('index.tools.openclaw.desc'),
    tag: t('index.tools.openclaw.tag'),
  },
  {
    name: t('index.tools.claudeCode.name'),
    icon: 'smart_display',
    desc: t('index.tools.claudeCode.desc'),
    tag: t('index.tools.claudeCode.tag'),
  },
  {
    name: t('index.tools.codex.name'),
    icon: 'developer_mode',
    desc: t('index.tools.codex.desc'),
    tag: t('index.tools.codex.tag'),
  },
  {
    name: t('index.tools.geminiCli.name'),
    icon: 'star',
    desc: t('index.tools.geminiCli.desc'),
    tag: t('index.tools.geminiCli.tag'),
  },
])

const features = computed<Array<{ title: string; desc: string; icon: IconName }>>(() => [
  {
    title: t('index.features.globalCoverage.title'),
    desc: t('index.features.globalCoverage.desc'),
    icon: 'language',
  },
  {
    title: t('index.features.highAvailability.title'),
    desc: t('index.features.highAvailability.desc'),
    icon: 'verified_user',
  },
  {
    title: t('index.features.easyIntegration.title'),
    desc: t('index.features.easyIntegration.desc'),
    icon: 'terminal',
  },
  {
    title: t('index.features.completeAudit.title'),
    desc: t('index.features.completeAudit.desc'),
    icon: 'description',
  },
])

const faqs = computed(() => [
  { q: t('index.faq.q1.q'), a: t('index.faq.q1.a') },
  { q: t('index.faq.q2.q'), a: t('index.faq.q2.a') },
  { q: t('index.faq.q3.q'), a: t('index.faq.q3.a') },
  { q: t('index.faq.q4.q'), a: t('index.faq.q4.a') },
  { q: t('index.faq.q5.q'), a: t('index.faq.q5.a') },
])

const openFaq = ref<number | null>(null)

function toggleFaq(idx: number) {
  openFaq.value = openFaq.value === idx ? null : idx
}

onMounted(() => {
  authStore.checkAuth()
  if (!appStore.publicSettingsLoaded) {
    appStore.fetchPublicSettings()
  }
})
</script>

<style scoped>
.index-page {
  font-feature-settings: 'kern' 1;
  -webkit-font-smoothing: antialiased;
}
</style>
