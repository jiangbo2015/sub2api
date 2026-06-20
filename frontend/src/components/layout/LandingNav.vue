<template>
  <header class="sticky top-0 z-50 border-b border-primary-100/40 bg-primary-50 backdrop-blur-md dark:border-dark-700/50 dark:bg-dark-900/90">
    <nav class="mx-auto flex max-w-6xl items-center justify-between px-6 py-4">
      <!-- Logo -->
      <router-link to="/home" class="flex shrink-0 items-center gap-2">
        <div class="h-10 w-full  overflow-hidden rounded-lg sm:h-12">
          <img :src="siteLogo || '/logo.svg'" alt="Logo" class="h-full w-full object-contain" />
        </div>
        <span class="text-lg font-bold text-primary-800 dark:text-primary-200">{{ siteName }}</span>
      </router-link>

      <!-- Desktop Nav Links -->
      <div class="hidden items-center gap-8 md:flex">
        <router-link to="/model-pricing" class="text-sm font-medium text-gray-600 transition-colors hover:text-primary-700 dark:text-gray-300 dark:hover:text-primary-400">{{ t('landing.nav.modelPricing') }}</router-link>
        <router-link to="/docs" class="text-sm font-medium text-gray-600 transition-colors hover:text-primary-700 dark:text-gray-300 dark:hover:text-primary-400">{{ t('landing.nav.docs') }}</router-link>
        <a href="/home#faq" class="text-sm font-medium text-gray-600 transition-colors hover:text-primary-700 dark:text-gray-300 dark:hover:text-primary-400" @click.prevent="navigateToFaq">{{ t('landing.nav.faq') }}</a>
        <a v-if="contactUrl" :href="contactUrl" target="_blank" rel="noopener noreferrer" class="text-sm font-medium text-gray-600 transition-colors hover:text-primary-700 dark:text-gray-300 dark:hover:text-primary-400">{{ t('landing.nav.contact') }}</a>
      </div>

      <!-- Right Actions -->
      <div class="flex shrink-0 items-center gap-2">
        <!-- Language Switcher -->
        <LocaleSwitcher />

        <!-- Theme Toggle -->
        <button
          class="rounded-lg p-2 text-gray-500 transition-colors hover:bg-gray-100 hover:text-gray-700 dark:text-gray-400 dark:hover:bg-dark-800 dark:hover:text-white"
          @click="toggleTheme"
          :title="isDark ? '切换到浅色模式' : '切换到深色模式'"
        >
          <Icon v-if="isDark" name="sun" size="sm" />
          <Icon v-else name="moon" size="sm" />
        </button>

        <!-- Console Button -->
        <router-link
          :to="isAuthenticated ? dashboardPath : '/login'"
          class="hidden rounded-full bg-primary-700 px-5 py-2 text-sm font-medium text-white transition-colors hover:bg-primary-800 sm:inline-flex"
        >
          {{ isAuthenticated ? t('home.dashboard') : t('home.login') }}
        </router-link>

        <!-- Mobile Hamburger -->
        <button class="ml-1 rounded-lg p-2 text-gray-600 transition-colors hover:bg-primary-50 hover:text-primary-700 dark:text-gray-400 dark:hover:bg-dark-800 md:hidden" @click="mobileMenuOpen = !mobileMenuOpen">
          <svg v-if="!mobileMenuOpen" class="h-5 w-5" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" d="M4 6h16M4 12h16M4 18h16" />
          </svg>
          <svg v-else class="h-5 w-5" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12" />
          </svg>
        </button>
      </div>
    </nav>

    <!-- Mobile Menu -->
    <div v-show="mobileMenuOpen" class="border-t border-primary-100/40  px-6 pb-4 pt-2 dark:border-dark-700/50 bg-primary-100 dark:bg-dark-900 md:hidden">
      <div class="flex flex-col gap-1">
        <router-link to="/model-pricing" class="rounded-lg px-3 py-2.5 text-sm font-medium text-gray-700 transition-colors hover:bg-primary-50 hover:text-primary-700 dark:text-gray-300 dark:hover:bg-dark-800" @click="mobileMenuOpen = false">{{ t('landing.nav.modelPricing') }}</router-link>
        <router-link to="/docs" class="rounded-lg px-3 py-2.5 text-sm font-medium text-gray-700 transition-colors hover:bg-primary-50 hover:text-primary-700 dark:text-gray-300 dark:hover:bg-dark-800" @click="mobileMenuOpen = false">{{ t('landing.nav.docs') }}</router-link>
        <a href="/home#faq" class="rounded-lg px-3 py-2.5 text-sm font-medium text-gray-700 transition-colors hover:bg-primary-50 hover:text-primary-700 dark:text-gray-300 dark:hover:bg-dark-800" @click.prevent="navigateToFaq">{{ t('landing.nav.faq') }}</a>
        <a v-if="contactUrl" :href="contactUrl" target="_blank" rel="noopener noreferrer" class="rounded-lg px-3 py-2.5 text-sm font-medium text-gray-700 transition-colors hover:bg-primary-50 hover:text-primary-700 dark:text-gray-300 dark:hover:bg-dark-800" @click="mobileMenuOpen = false">{{ t('landing.nav.contact') }}</a>
        <router-link
          :to="isAuthenticated ? dashboardPath : '/login'"
          class="mt-2 block rounded-xl bg-primary-700 px-3 py-2.5 text-center text-sm font-medium text-white transition-colors hover:bg-primary-800"
          @click="mobileMenuOpen = false"
        >
          {{ isAuthenticated ? t('home.dashboard') : t('home.login') }}
        </router-link>
      </div>
    </div>
  </header>
</template>

<script setup lang="ts">
import { ref, computed, onMounted } from 'vue'
import { useRoute, useRouter } from 'vue-router'
import { useI18n } from 'vue-i18n'
import { useAuthStore, useAppStore } from '@/stores'
import Icon from '@/components/icons/Icon.vue'
import LocaleSwitcher from '@/components/common/LocaleSwitcher.vue'

const route = useRoute()
const router = useRouter()
const { t } = useI18n()
const authStore = useAuthStore()
const appStore = useAppStore()

const siteName = computed(() => appStore.cachedPublicSettings?.site_name || appStore.siteName || 'PineAI.me')
const siteLogo = computed(() => appStore.cachedPublicSettings?.site_logo || appStore.siteLogo || '')
const contactUrl = computed(() => appStore.cachedPublicSettings?.contact_info || '')

const isAuthenticated = computed(() => authStore.isAuthenticated)
const isAdmin = computed(() => authStore.isAdmin)
const dashboardPath = computed(() => isAdmin.value ? '/admin/dashboard' : '/dashboard')

const mobileMenuOpen = ref(false)
const isDark = ref(document.documentElement.classList.contains('dark'))

function toggleTheme() {
  isDark.value = !isDark.value
  document.documentElement.classList.toggle('dark', isDark.value)
  localStorage.setItem('theme', isDark.value ? 'dark' : 'light')
}

function scrollToFaq() {
  document.getElementById('faq')?.scrollIntoView({ behavior: 'smooth' })
}

function navigateToFaq() {
  mobileMenuOpen.value = false

  if (route.path === '/home') {
    scrollToFaq()
    router.replace({ path: '/home', hash: '#faq' })
    return
  }

  router.push({ path: '/home', hash: '#faq' })
}

onMounted(() => {
  const savedTheme = localStorage.getItem('theme')
  if (
    savedTheme === 'dark' ||
    (!savedTheme && window.matchMedia('(prefers-color-scheme: dark)').matches)
  ) {
    isDark.value = true
    document.documentElement.classList.add('dark')
  }
})
</script>
