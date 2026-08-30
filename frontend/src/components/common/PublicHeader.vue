<template>
  <header class="border-b border-gray-200 px-4 py-4 sm:px-6 dark:border-dark-800">
    <nav class="mx-auto flex max-w-5xl flex-wrap items-center justify-between gap-3 sm:gap-4">
      <router-link to="/home" class="flex min-w-0 flex-1 items-center gap-3">
        <img
          :src="siteLogo || '/logo.svg'"
          alt="Logo"
          class="h-9 w-9 shrink-0 rounded-lg object-contain"
        />
        <span class="min-w-0 truncate text-base font-semibold">{{ siteName }}</span>
      </router-link>

      <div class="flex max-w-full shrink-0 flex-wrap items-center justify-end gap-2">
        <LocaleSwitcher />

        <nav class="hidden items-center gap-1 sm:flex">
          <router-link
            v-if="showModelPlazaEntry"
            to="/model-plaza"
            class="inline-flex items-center gap-1.5 rounded-lg px-2.5 py-2 text-sm font-medium text-gray-600 transition-colors hover:bg-gray-100 hover:text-gray-900 dark:text-dark-400 dark:hover:bg-dark-800 dark:hover:text-white"
          >
            {{ t('nav.modelPricing') }}
          </router-link>
          <router-link
            to="/model-pricing"
            class="inline-flex items-center gap-1.5 rounded-lg px-2.5 py-2 text-sm font-medium text-gray-600 transition-colors hover:bg-gray-100 hover:text-gray-900 dark:text-dark-400 dark:hover:bg-dark-800 dark:hover:text-white"
          >
            {{ t('nav.modelPricing') }}
          </router-link>
          <router-link
            to="/docs"
            class="inline-flex items-center gap-1.5 rounded-lg px-2.5 py-2 text-sm font-medium text-gray-600 transition-colors hover:bg-gray-100 hover:text-gray-900 dark:text-dark-400 dark:hover:bg-dark-800 dark:hover:text-white"
            :title="t('home.viewDocs')"
          >
            {{ t('nav.docsUsage') }}
          </router-link>
          <router-link
            to="/contact"
            class="inline-flex items-center gap-1.5 rounded-lg px-2.5 py-2 text-sm font-medium text-gray-600 transition-colors hover:bg-gray-100 hover:text-gray-900 dark:text-dark-400 dark:hover:bg-dark-800 dark:hover:text-white"
          >
            {{ t('nav.contactUs') }}
          </router-link>
        </nav>

        <button
          class="flex h-10 w-10 shrink-0 items-center justify-center rounded-lg text-gray-500 hover:bg-gray-100 dark:text-dark-400 dark:hover:bg-dark-800"
          :title="isDark ? t('home.switchToLight') : t('home.switchToDark')"
          @click="toggleTheme"
        >
          <Icon v-if="isDark" name="sun" size="md" />
          <Icon v-else name="moon" size="md" />
        </button>

        <router-link
          :to="loginDestination"
          class="inline-flex min-h-10 shrink-0 items-center justify-center rounded-lg bg-gray-900 px-4 py-2 text-sm font-medium text-white hover:bg-gray-800 dark:bg-white dark:text-gray-900 dark:hover:bg-gray-200"
        >
          {{ loginText }}
        </router-link>
      </div>
    </nav>
  </header>
</template>

<script setup lang="ts">
import { computed, onMounted, ref } from 'vue'
import { useI18n } from 'vue-i18n'
import { useAppStore } from '@/stores'
import LocaleSwitcher from '@/components/common/LocaleSwitcher.vue'
import Icon from '@/components/icons/Icon.vue'

withDefaults(
  defineProps<{
    showModelPlazaEntry?: boolean
    loginDestination?: string
    loginText?: string
  }>(),
  {
    showModelPlazaEntry: false,
    loginDestination: '/login',
    loginText: 'Login'
  }
)

const { t } = useI18n()
const appStore = useAppStore()

const siteName = computed(() => appStore.cachedPublicSettings?.site_name || appStore.siteName || 'Sub2API')
const siteLogo = computed(() => appStore.cachedPublicSettings?.site_logo || appStore.siteLogo || '/logo.svg')
const isDark = ref(document.documentElement.classList.contains('dark'))

function initTheme() {
  const savedTheme = localStorage.getItem('theme')
  const shouldUseDark =
    savedTheme === 'dark' ||
    (!savedTheme && window.matchMedia('(prefers-color-scheme: dark)').matches)

  document.documentElement.classList.toggle('dark', shouldUseDark)
  isDark.value = shouldUseDark
}

function toggleTheme() {
  const root = document.documentElement
  const nextDark = !root.classList.contains('dark')
  root.classList.toggle('dark', nextDark)
  isDark.value = nextDark
  localStorage.setItem('theme', nextDark ? 'dark' : 'light')
}

onMounted(() => {
  initTheme()
})
</script>
