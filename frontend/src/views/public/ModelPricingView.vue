<template>
  <div class="relative flex min-h-screen flex-col bg-gray-50 dark:bg-dark-950">
    <PublicHeader :login-destination="'/login'" :login-text="t('home.login')" />

    <main class="mx-auto flex w-full max-w-5xl flex-1 flex-col px-6 py-12 sm:py-16">
      <div class="mb-10 text-center">
        <p class="mb-4 text-sm font-medium uppercase tracking-[0.2em] text-primary-600 dark:text-primary-400">
          Pricing
        </p>
        <h1 class="text-3xl font-bold tracking-tight text-gray-900 dark:text-white sm:text-4xl">
          模型价格
        </h1>
        <p class="mt-4 text-base text-gray-600 dark:text-dark-300">
          当前支持 Claude 和 GPT 模型，价格与官方保持一致，点击下方入口可查看官方定价。
        </p>
      </div>

      <div class="grid gap-6 md:grid-cols-2">
        <a
          href="https://platform.claude.com/docs/en/about-claude/pricing"
          target="_blank"
          rel="noopener noreferrer"
          class="group rounded-2xl border border-gray-200 bg-white p-8 shadow-sm transition hover:-translate-y-0.5 hover:shadow-md dark:border-dark-700 dark:bg-dark-900"
        >
          <div class="mb-5 flex h-12 w-12 items-center justify-center rounded-xl bg-primary-50 text-primary-600 dark:bg-primary-900/20 dark:text-primary-400">
            <Icon name="sparkles" size="md" />
          </div>
          <p class="text-sm font-medium uppercase tracking-[0.15em] text-gray-500 dark:text-dark-400">
            Claude
          </p>
          <h2 class="mt-3 text-2xl font-bold text-gray-900 dark:text-white">官方价格</h2>
          <p class="mt-3 text-sm text-gray-600 dark:text-dark-300">
            查看 Claude 官方价格与计费说明。
          </p>
          <div class="mt-6 inline-flex items-center gap-2 text-sm font-semibold text-primary-600 dark:text-primary-400">
            立即查看
            <Icon name="arrowRight" size="sm" />
          </div>
        </a>

        <a
          href="https://developers.openai.com/api/docs/pricing?latest-pricing=standard"
          target="_blank"
          rel="noopener noreferrer"
          class="group rounded-2xl border border-gray-200 bg-white p-8 shadow-sm transition hover:-translate-y-0.5 hover:shadow-md dark:border-dark-700 dark:bg-dark-900"
        >
          <div class="mb-5 flex h-12 w-12 items-center justify-center rounded-xl bg-primary-50 text-primary-600 dark:bg-primary-900/20 dark:text-primary-400">
            <Icon name="brain" size="md" />
          </div>
          <p class="text-sm font-medium uppercase tracking-[0.15em] text-gray-500 dark:text-dark-400">
            GPT
          </p>
          <h2 class="mt-3 text-2xl font-bold text-gray-900 dark:text-white">官方价格</h2>
          <p class="mt-3 text-sm text-gray-600 dark:text-dark-300">
            查看 OpenAI 官方 API 定价与标准价格表。
          </p>
          <div class="mt-6 inline-flex items-center gap-2 text-sm font-semibold text-primary-600 dark:text-primary-400">
            立即查看
            <Icon name="arrowRight" size="sm" />
          </div>
        </a>
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
