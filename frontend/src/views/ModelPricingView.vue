<template>
  <div class="min-h-screen bg-primary-100 dark:bg-dark-900">
    <LandingNav />

    <div class="mx-auto max-w-6xl px-6 py-8">
      <!-- Header -->
      <div class="mb-8">
        <h1 class="text-3xl font-bold text-gray-900 dark:text-white">{{ t('modelPricing.title') }}</h1>
        <p class="mt-2 text-gray-600 dark:text-dark-300">{{ t('modelPricing.description') }}</p>
      </div>

      <!-- Model Selection Tabs -->
      <div class="mb-6 flex gap-2 border-b border-gray-200 dark:border-dark-700">
        <button
          v-for="model in modelTabs"
          :key="model.id"
          @click="selectedModel = model.id"
          :class="[
            'px-4 py-2 text-sm font-medium transition-colors',
            selectedModel === model.id
              ? 'border-b-2 border-primary-500 text-primary-600 dark:text-primary-400'
              : 'text-gray-600 hover:text-gray-900 dark:text-dark-400 dark:hover:text-white'
          ]"
        >
          {{ model.name }}
        </button>
      </div>

      <!-- Pricing Rules -->
      <div class="mb-6 rounded-lg bg-blue-50 p-4 dark:bg-blue-900/20">
        <h3 class="mb-2 font-semibold text-gray-900 dark:text-white">{{ t('modelPricing.pricingRules') }}</h3>
        <p class="text-sm text-gray-700 dark:text-dark-300">{{ t('modelPricing.pricingRulesText') }}</p>
        <p class="mt-1 text-sm text-gray-600 dark:text-dark-400">
          {{ t('modelPricing.example') }}: claude-opus-4-8 {{ t('modelPricing.inputPrice') }}, {{ t('modelPricing.official') }} ¥35.00, {{ t('modelPricing.groupPrice') }} ¥5.00
        </p>
      </div>

      <!-- Price List Section -->
      <div class="rounded-lg bg-white p-6 shadow-sm dark:bg-dark-800">
        <div class="mb-4 flex items-center justify-between">
          <h3 class="text-lg font-semibold text-gray-900 dark:text-white">{{ t('modelPricing.priceList') }}</h3>
          <!-- Toggle Buttons -->
          <div class="flex rounded-lg border border-gray-200 dark:border-dark-700">
            <button
              @click="priceView = 'group'"
              :class="[
                'px-4 py-2 text-sm font-medium transition-colors',
                priceView === 'group'
                  ? 'bg-primary-500 text-white'
                  : 'bg-white text-gray-700 hover:bg-gray-50 dark:bg-dark-800 dark:text-dark-300 dark:hover:bg-dark-700'
              ]"
            >
              {{ t('modelPricing.groupPrice') }}
            </button>
            <button
              @click="priceView = 'official'"
              :class="[
                'px-4 py-2 text-sm font-medium transition-colors',
                priceView === 'official'
                  ? 'bg-primary-500 text-white'
                  : 'bg-white text-gray-700 hover:bg-gray-50 dark:bg-dark-800 dark:text-dark-300 dark:hover:bg-dark-700'
              ]"
            >
              {{ t('modelPricing.officialPrice') }}
            </button>
          </div>
        </div>

        <p class="mb-4 text-sm text-gray-600 dark:text-dark-400">
          {{ t('modelPricing.priceListNote') }}
        </p>

        <!-- Group Tabs -->
        <div v-if="priceView === 'group'" class="mb-6">
          <div class="mb-4 flex gap-2 border-b border-gray-200 dark:border-dark-700">
            <button
              v-for="group in groupInfo"
              :key="group.id"
              @click="selectedGroup = group.id"
              :class="[
                'px-4 py-2 text-sm font-medium transition-colors',
                selectedGroup === group.id
                  ? 'border-b-2 border-primary-500 text-primary-600 dark:text-primary-400'
                  : 'text-gray-600 hover:text-gray-900 dark:text-dark-400 dark:hover:text-white'
              ]"
            >
              {{ group.name }}
            </button>
          </div>
          
          <!-- Selected Group Info -->
          <div class="rounded-lg bg-gray-50 p-4 dark:bg-dark-700/30">
            <div class="flex items-center justify-between text-sm">
              <span class="font-medium text-gray-900 dark:text-white">
                {{ groupInfo.find(g => g.id === selectedGroup)?.name }}
              </span>
              <span class="text-gray-600 dark:text-dark-400">
                {{ t('modelPricing.discount') }}: {{ groupInfo.find(g => g.id === selectedGroup)?.discount }} | {{ t('modelPricing.multiplier') }}: {{ groupInfo.find(g => g.id === selectedGroup)?.multiplier }}
              </span>
            </div>
          </div>
        </div>

        <!-- Pricing Table -->
        <div class="overflow-x-auto">
          <table class="w-full text-sm">
            <thead>
              <tr class="border-b border-gray-200 dark:border-dark-700">
                <th class="px-4 py-3 text-left font-medium text-gray-900 dark:text-white">{{ t('modelPricing.modelId') }}</th>
                <th class="px-4 py-3 text-left font-medium text-gray-900 dark:text-white">{{ t('modelPricing.inputPrice') }}</th>
                <th class="px-4 py-3 text-left font-medium text-gray-900 dark:text-white">{{ t('modelPricing.outputPrice') }}</th>
                <th class="px-4 py-3 text-left font-medium text-gray-900 dark:text-white">{{ t('modelPricing.cacheCreation') }}</th>
                <th class="px-4 py-3 text-left font-medium text-gray-900 dark:text-white">{{ t('modelPricing.cacheRead') }}</th>
                <th class="px-4 py-3 text-left font-medium text-gray-900 dark:text-white">{{ t('modelPricing.modelDescription') }}</th>
              </tr>
            </thead>
            <tbody>
              <tr
                v-for="model in currentModelData"
                :key="model.id"
                class="border-b border-gray-100 dark:border-dark-800 hover:bg-gray-50 dark:hover:bg-dark-700/50"
              >
                <td class="px-4 py-3 font-mono text-gray-900 dark:text-white">{{ model.id }}</td>
                <td class="px-4 py-3 text-gray-700 dark:text-dark-300">
                  {{ priceView === 'group' ? model.groupPrice.input : model.officialPrice.input }}
                </td>
                <td class="px-4 py-3 text-gray-700 dark:text-dark-300">
                  {{ priceView === 'group' ? model.groupPrice.output : model.officialPrice.output }}
                </td>
                <td class="px-4 py-3 text-gray-700 dark:text-dark-300">
                  {{ priceView === 'group' ? model.groupPrice.cacheCreation : model.officialPrice.cacheCreation }}
                </td>
                <td class="px-4 py-3 text-gray-700 dark:text-dark-300">
                  {{ priceView === 'group' ? model.groupPrice.cacheRead : model.officialPrice.cacheRead }}
                </td>
                <td class="px-4 py-3 text-gray-600 dark:text-dark-400">{{ model.description }}</td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>

    <LandingFooter />
  </div>
</template>

<script setup lang="ts">
import { ref, computed, onMounted } from 'vue'
import { useI18n } from 'vue-i18n'
import { useAuthStore, useAppStore } from '@/stores'
import LandingNav from '@/components/layout/LandingNav.vue'
import LandingFooter from '@/components/layout/LandingFooter.vue'

const { t } = useI18n()

const authStore = useAuthStore()
const appStore = useAppStore()

// Model selection tabs
const modelTabs = [
  { id: 'claude-code', name: 'Claude Code' },
  { id: 'codex', name: 'Codex' },
  { id: 'gemini', name: 'Gemini' }
]

const selectedModel = ref('claude-code')
const priceView = ref<'group' | 'official'>('group')
const selectedGroup = ref('lite')

// Group information
const groupInfo = [
  { id: 'lite', name: 'Claude lite (特价)', discount: '90%', multiplier: '0.1' },
  { id: 'plus', name: 'Claude Plus (精品)', discount: '85%', multiplier: '0.15' },
  { id: 'max-cc', name: 'Claude Max (仅限CC)', discount: '80%', multiplier: '0.2' },
  { id: 'max-external', name: 'Claude Max (外接版)', discount: '75%', multiplier: '0.25' }
]

// Model pricing data (JSON structure)
const modelPricingData = {
  'claude-code': [
    {
      id: 'claude-opus-4-8',
      groupId: 'lite',
      officialPrice: {
        input: '¥35.00/1M',
        output: '¥175.00/1M',
        cacheCreation: '¥43.75/1M',
        cacheRead: '¥3.50/1M'
      },
      groupPrice: {
        input: '¥3.50/1M',
        output: '¥17.50/1M',
        cacheCreation: '¥4.38/1M',
        cacheRead: '¥0.35/1M'
      },
      description: 'Claude Opus 4.8'
    },
    {
      id: 'claude-opus-4-7',
      groupId: 'lite',
      officialPrice: {
        input: '¥35.00/1M',
        output: '¥175.00/1M',
        cacheCreation: '¥43.75/1M',
        cacheRead: '¥3.50/1M'
      },
      groupPrice: {
        input: '¥3.50/1M',
        output: '¥17.50/1M',
        cacheCreation: '¥4.38/1M',
        cacheRead: '¥0.35/1M'
      },
      description: 'Claude Opus 4.7'
    },
    {
      id: 'claude-opus-4-6',
      groupId: 'lite',
      officialPrice: {
        input: '¥35.00/1M',
        output: '¥175.00/1M',
        cacheCreation: '¥43.75/1M',
        cacheRead: '¥3.50/1M'
      },
      groupPrice: {
        input: '¥3.50/1M',
        output: '¥17.50/1M',
        cacheCreation: '¥4.38/1M',
        cacheRead: '¥0.35/1M'
      },
      description: 'Claude Opus 4.6'
    },
    {
      id: 'claude-sonnet-4-6',
      groupId: 'plus',
      officialPrice: {
        input: '¥21.00/1M',
        output: '¥105.00/1M',
        cacheCreation: '¥26.25/1M',
        cacheRead: '¥2.10/1M'
      },
      groupPrice: {
        input: '¥2.10/1M',
        output: '¥10.50/1M',
        cacheCreation: '¥2.63/1M',
        cacheRead: '¥0.21/1M'
      },
      description: 'Claude Sonnet 4.6'
    },
    {
      id: 'claude-haiku-4-5',
      groupId: 'lite',
      officialPrice: {
        input: '¥7.00/1M',
        output: '¥35.00/1M',
        cacheCreation: '¥8.75/1M',
        cacheRead: '¥0.70/1M'
      },
      groupPrice: {
        input: '¥0.70/1M',
        output: '¥3.50/1M',
        cacheCreation: '¥0.88/1M',
        cacheRead: '¥0.07/1M'
      },
      description: 'Claude Haiku 4.5'
    }
  ],
  'codex': [
    {
      id: 'codex-gpt-4',
      groupId: 'plus',
      officialPrice: {
        input: '¥21.00/1M',
        output: '¥105.00/1M',
        cacheCreation: '¥26.25/1M',
        cacheRead: '¥2.10/1M'
      },
      groupPrice: {
        input: '¥2.10/1M',
        output: '¥10.50/1M',
        cacheCreation: '¥2.63/1M',
        cacheRead: '¥0.21/1M'
      },
      description: 'Codex GPT-4'
    }
  ],
  'gemini': [
    {
      id: 'gemini-pro',
      groupId: 'lite',
      officialPrice: {
        input: '¥7.00/1M',
        output: '¥35.00/1M',
        cacheCreation: '¥8.75/1M',
        cacheRead: '¥0.70/1M'
      },
      groupPrice: {
        input: '¥0.70/1M',
        output: '¥3.50/1M',
        cacheCreation: '¥0.88/1M',
        cacheRead: '¥0.07/1M'
      },
      description: 'Gemini Pro'
    }
  ]
}

// Computed property for current model data
const currentModelData = computed(() => {
  const allModels = modelPricingData[selectedModel.value as keyof typeof modelPricingData] || []
  
  // Filter by group when in group view
  if (priceView.value === 'group') {
    return allModels.filter(model => model.groupId === selectedGroup.value)
  }
  
  // Show all models when in official view
  return allModels
})

onMounted(() => {
  authStore.checkAuth()
  if (!appStore.publicSettingsLoaded) {
    appStore.fetchPublicSettings()
  }
})
</script>
