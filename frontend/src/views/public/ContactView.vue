<template>
  <div class="relative flex min-h-screen flex-col bg-gray-50 dark:bg-dark-950">
    <PublicHeader :login-destination="'/login'" :login-text="t('home.login')" />

    <main class="mx-auto flex w-full max-w-5xl flex-1 flex-col px-6 py-12 sm:py-16">
      <div class="mb-10 text-center">
        <p class="mb-4 text-sm font-medium uppercase tracking-[0.2em] text-primary-600 dark:text-primary-400">
          Contact
        </p>
        <h1 class="text-3xl font-bold tracking-tight text-gray-900 dark:text-white sm:text-4xl">
          联系我们
        </h1>
        <p class="mt-4 text-base text-gray-600 dark:text-dark-300">
          如有问题或合作需求，请通过以下方式联系我们。
        </p>
      </div>

      <div class="grid gap-6 md:grid-cols-2">
        <div class="rounded-2xl border border-gray-200 bg-white p-8 shadow-sm dark:border-dark-700 dark:bg-dark-900">
          <div class="mb-4 flex h-12 w-12 items-center justify-center rounded-xl bg-primary-50 text-primary-600 dark:bg-primary-900/20 dark:text-primary-400">
            <Icon name="chatBubble" size="md" />
          </div>
          <p class="text-sm font-medium uppercase tracking-[0.15em] text-gray-500 dark:text-dark-400">
            客服 QQ
          </p>
          <a
            href="http://wpa.qq.com/msgrd?v=3&uin=772051431&site=qq&menu=yes"
            target="_blank"
            rel="noopener noreferrer"
            class="mt-4 block text-2xl font-semibold text-gray-900 transition-colors hover:text-primary-600 dark:text-white dark:hover:text-primary-400"
          >
            772051431
          </a>
        </div>

        <div class="rounded-2xl border border-gray-200 bg-white p-8 shadow-sm dark:border-dark-700 dark:bg-dark-900">
          <div class="mb-4 flex h-12 w-12 items-center justify-center rounded-xl bg-primary-50 text-primary-600 dark:bg-primary-900/20 dark:text-primary-400">
            <Icon name="mail" size="md" />
          </div>
          <p class="text-sm font-medium uppercase tracking-[0.15em] text-gray-500 dark:text-dark-400">
            邮箱
          </p>
          <a
            href="mailto:support@pineai.net"
            class="mt-4 block break-all text-xl font-semibold text-gray-900 transition-colors hover:text-primary-600 dark:text-white dark:hover:text-primary-400"
          >
            support@pineai.net
          </a>
        </div>
      </div>
    </main>
  </div>
</template>

<script setup lang="ts">
import { useI18n } from 'vue-i18n'
import PublicHeader from '@/components/common/PublicHeader.vue'
import Icon from '@/components/icons/Icon.vue'

const { t } = useI18n()
</script>
