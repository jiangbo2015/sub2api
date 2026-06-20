<template>
  <footer class="border-t border-gray-200/60 px-6 py-8 dark:border-dark-700/60">
    <div class="mx-auto flex max-w-6xl flex-col items-center justify-between gap-4 sm:flex-row">
      <router-link to="/home" class="flex items-center gap-2">
        <div class="h-8 w-full max-w-[2rem] overflow-hidden rounded-md sm:h-10 sm:max-w-[2.5rem]">
          <img :src="siteLogo || '/logo.svg'" alt="Logo" class="h-full w-full object-contain" />
        </div>
        <!-- <span class="text-sm font-semibold text-primary-800 dark:text-primary-200">{{ siteName }}</span> -->
      </router-link>
      <p class="text-xs text-gray-400 dark:text-dark-500">
        &copy; {{ currentYear }} {{ siteName }}. {{ t('index.footer.allRightsReserved') }}
      </p>
    </div>
  </footer>
</template>

<script setup lang="ts">
import { computed } from 'vue'
import { useI18n } from 'vue-i18n'
import { useAppStore } from '@/stores'

const { t } = useI18n()
const appStore = useAppStore()

const siteName = computed(() => appStore.cachedPublicSettings?.site_name || appStore.siteName || 'PineA.me')
const siteLogo = computed(() => appStore.cachedPublicSettings?.site_logo || appStore.siteLogo || '')
const currentYear = computed(() => new Date().getFullYear())
</script>
