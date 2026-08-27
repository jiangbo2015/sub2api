<template>
  <div class="min-h-screen bg-slate-50 text-slate-900 dark:bg-slate-950 dark:text-slate-100">
    <LandingNav />

    <main class="mx-auto max-w-7xl px-4 py-8 sm:px-6 lg:px-8">
      <div class="mb-8 rounded-2xl border border-slate-200 bg-white p-6 shadow-sm dark:border-slate-700 dark:bg-slate-900">
        <div class="flex flex-col gap-3 md:flex-row md:items-end md:justify-between">
          <div>
            <p class="mb-2 text-sm font-medium uppercase tracking-[0.18em] text-primary-600 dark:text-primary-400">
              Model pricing
            </p>
            <h1 class="text-3xl font-bold tracking-tight sm:text-4xl">模型价格</h1>
          </div>
          <div class="rounded-full bg-blue-50 px-4 py-2 text-sm text-blue-700 dark:bg-blue-500/10 dark:text-blue-300">
            价格参考官方定价，实际可按需开放其他模型
          </div>
        </div>
      </div>

      <section class="mb-8 grid gap-4 md:grid-cols-2">
        <div class="rounded-2xl border border-slate-200 bg-white p-6 shadow-sm dark:border-slate-700 dark:bg-slate-900">
          <div class="mb-4 flex items-center justify-between">
            <h2 class="text-xl font-semibold">当前支持的模型</h2>
            <span class="rounded-full bg-slate-100 px-3 py-1 text-xs font-medium text-slate-600 dark:bg-slate-800 dark:text-slate-300">
              {{ modelGroups.length }} 个系列
            </span>
          </div>

          <div class="flex gap-2">
            <button
              v-for="group in modelGroups"
              :key="group.id"
              type="button"
              @click="activeCategory = group.id"
              :class="[
                'rounded-full px-4 py-2 text-sm font-medium transition-all',
                activeCategory === group.id
                  ? 'bg-primary-600 text-white shadow-sm'
                  : 'bg-slate-100 text-slate-700 hover:bg-slate-200 dark:bg-slate-800 dark:text-slate-200 dark:hover:bg-slate-700'
              ]"
            >
              {{ group.name }}
            </button>
          </div>
        </div>

        <div class="rounded-2xl border border-slate-200 bg-white p-6 shadow-sm dark:border-slate-700 dark:bg-slate-900">
          <h2 class="mb-4 text-xl font-semibold">官方价格参考</h2>
          <div class="flex flex-wrap gap-3">
            <a
              href="https://platform.claude.com/docs/en/about-claude/pricing"
              target="_blank"
              rel="noreferrer"
              class="inline-flex items-center rounded-lg border border-slate-200 bg-slate-50 px-4 py-2 text-sm font-medium text-slate-700 transition hover:border-primary-200 hover:bg-primary-50 hover:text-primary-700 dark:border-slate-700 dark:bg-slate-800 dark:text-slate-200 dark:hover:border-primary-600 dark:hover:text-primary-300"
            >
              Claude 官方价格
            </a>
            <a
              href="https://developers.openai.com/api/docs/pricing?latest-pricing=standard"
              target="_blank"
              rel="noreferrer"
              class="inline-flex items-center rounded-lg border border-slate-200 bg-slate-50 px-4 py-2 text-sm font-medium text-slate-700 transition hover:border-primary-200 hover:bg-primary-50 hover:text-primary-700 dark:border-slate-700 dark:bg-slate-800 dark:text-slate-200 dark:hover:border-primary-600 dark:hover:text-primary-300"
            >
              GPT 官方价格
            </a>
          </div>
        </div>
      </section>

      <section class="mb-8 rounded-2xl border border-slate-200 bg-white p-6 shadow-sm dark:border-slate-700 dark:bg-slate-900">
        <div class="mb-5 flex items-center justify-between gap-3">
          <h2 class="text-xl font-semibold">{{ activeGroup.name }} 模型列表</h2>
          <span class="rounded-full bg-emerald-50 px-3 py-1 text-xs font-medium text-emerald-700 dark:bg-emerald-500/10 dark:text-emerald-300">
            参考官方价格</span>
        </div>

        <div class="grid gap-3 sm:grid-cols-2 xl:grid-cols-3">
          <div
            v-for="model in activeModels"
            :key="model.id"
            class="rounded-xl border border-slate-200 bg-slate-50 p-4 transition hover:border-primary-200 hover:shadow-sm dark:border-slate-700 dark:bg-slate-800/80"
          >
            <div class="mb-3 flex items-center justify-between">
              <span class="font-mono text-sm font-semibold text-slate-900 dark:text-white">{{ model.id }}</span>
              <span class="rounded-full bg-primary-50 px-2 py-1 text-[10px] font-medium text-primary-700 dark:bg-primary-500/10 dark:text-primary-300">
                {{ model.label }}
              </span>
            </div>

            <div class="space-y-2 text-sm text-slate-600 dark:text-slate-300">
              <div class="flex items-center justify-between">
                <span>输入</span>
                <strong class="text-slate-900 dark:text-white">{{ formatPrice(model.officialPrice.input) }}</strong>
              </div>
              <div class="flex items-center justify-between">
                <span>输出</span>
                <strong class="text-slate-900 dark:text-white">{{ formatPrice(model.officialPrice.output) }}</strong>
              </div>
              <div v-if="model.officialPrice.cacheCreation !== null" class="flex items-center justify-between">
                <span>缓存创建</span>
                <strong class="text-slate-900 dark:text-white">{{ formatPrice(model.officialPrice.cacheCreation) }}</strong>
              </div>
              <div v-if="model.officialPrice.cacheRead !== null" class="flex items-center justify-between">
                <span>缓存读取</span>
                <strong class="text-slate-900 dark:text-white">{{ formatPrice(model.officialPrice.cacheRead) }}</strong>
              </div>
            </div>
          </div>
        </div>
      </section>

      <section class="rounded-2xl border border-slate-200 bg-white p-6 shadow-sm dark:border-slate-700 dark:bg-slate-900">
        <div class="mb-4 flex items-center justify-between">
          <h2 class="text-xl font-semibold">价格说明</h2>
          <span class="text-sm text-slate-500 dark:text-slate-400">单位：¥/1M</span>
        </div>

        <div class="overflow-x-auto">
          <table class="min-w-full text-left text-sm">
            <thead>
              <tr class="border-b border-slate-200 text-slate-700 dark:border-slate-700 dark:text-slate-300">
                <th class="px-3 py-3 font-medium">模型</th>
                <th class="px-3 py-3 font-medium">输入</th>
                <th class="px-3 py-3 font-medium">输出</th>
                <th class="px-3 py-3 font-medium">缓存创建</th>
                <th class="px-3 py-3 font-medium">缓存读取</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="model in activeModels" :key="model.id" class="border-b border-slate-100 dark:border-slate-800">
                <td class="px-3 py-3 font-mono text-slate-900 dark:text-white">{{ model.id }}</td>
                <td class="px-3 py-3">{{ formatPrice(model.officialPrice.input) }}</td>
                <td class="px-3 py-3">{{ formatPrice(model.officialPrice.output) }}</td>
                <td class="px-3 py-3">{{ formatPrice(model.officialPrice.cacheCreation) }}</td>
                <td class="px-3 py-3">{{ formatPrice(model.officialPrice.cacheRead) }}</td>
              </tr>
            </tbody>
          </table>
        </div>

        <div class="mt-6 rounded-xl bg-amber-50 p-4 text-sm text-amber-800 dark:bg-amber-500/10 dark:text-amber-200">
          目前已支持 Claude 与 GPT 两类模型，可根据业务需要继续开放其他模型；
        </div>
      </section>
    </main>

    <LandingFooter />
  </div>
</template>

<script setup lang="ts">
import { ref, computed, onMounted } from 'vue'
import { useAuthStore } from '@/stores'
import LandingNav from '@/components/layout/LandingNav.vue'
import LandingFooter from '@/components/layout/LandingFooter.vue'

const authStore = useAuthStore()

const modelGroups = [
  { id: 'claude', name: 'Claude' },
  { id: 'gpt', name: 'GPT' }
] as const

const activeCategory = ref<(typeof modelGroups)[number]['id']>('claude')

const claudeModels = [
  {
    id: 'claude-opus-5',
    label: 'Opus',
    officialPrice: { input: 35, output: 175, cacheCreation: 43.75, cacheRead: 3.5 }
  },
  {
    id: 'claude-opus-4-8',
    label: 'Opus',
    officialPrice: { input: 35, output: 175, cacheCreation: 43.75, cacheRead: 3.5 }
  },
  {
    id: 'claude-opus-4-7',
    label: 'Opus',
    officialPrice: { input: 35, output: 175, cacheCreation: 43.75, cacheRead: 3.5 }
  },
  {
    id: 'claude-opus-4-6',
    label: 'Opus',
    officialPrice: { input: 35, output: 175, cacheCreation: 43.75, cacheRead: 3.5 }
  },
  {
    id: 'claude-sonnet-4-6',
    label: 'Sonnet',
    officialPrice: { input: 21, output: 105, cacheCreation: 26.25, cacheRead: 2.1 }
  },
  {
    id: 'claude-haiku-4-5',
    label: 'Haiku',
    officialPrice: { input: 7, output: 35, cacheCreation: 8.75, cacheRead: 0.7 }
  }
] as const

const gptModels = [
  {
    id: 'gpt-5.6-sol',
    label: 'GPT-5.6 Sol',
    officialPrice: { input: 4, output: 20, cacheCreation: 5, cacheRead: 0.4 }
  },
  {
    id: 'gpt-5.6-terra',
    label: 'GPT-5.6 Terra',
    officialPrice: { input: 2, output: 12, cacheCreation: 2.5, cacheRead: 0.2 }
  },
  {
    id: 'gpt-5.6-luna',
    label: 'GPT-5.6 Luna',
    officialPrice: { input: 0.2, output: 1.2, cacheCreation: 0.25, cacheRead: 0.02 }
  },
  {
    id: 'gpt-5.5',
    label: 'GPT-5.5',
    officialPrice: { input: 5, output: 30, cacheCreation: null, cacheRead: 0.5 }
  },
  {
    id: 'gpt-5.4',
    label: 'GPT-5.4',
    officialPrice: { input: 2.5, output: 15, cacheCreation: null, cacheRead: 0.25 }
  },
  {
    id: 'gpt-5.4-mini',
    label: 'GPT-5.4 Mini',
    officialPrice: { input: 0.75, output: 4.5, cacheCreation: null, cacheRead: 0.075 }
  },
] as const

const activeGroup = computed(
  () => modelGroups.find((group) => group.id === activeCategory.value) ?? modelGroups[0]
)

const activeModels = computed(() => {
  return activeCategory.value === 'claude' ? claudeModels : gptModels
})

const formatPrice = (value: number | null) => {
  if (value === null) return '—'
  return `$${value.toFixed(2)}`
}

onMounted(() => {
  authStore.checkAuth()
})
</script>
