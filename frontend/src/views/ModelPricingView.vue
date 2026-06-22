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
          {{ t('modelPricing.example') }}: claude-opus-4-8 {{ t('modelPricing.inputPrice') }}, {{ t('modelPricing.official') }} ¥35.00, {{ t('modelPricing.groupPrice') }} ¥28.00
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
              v-for="group in activeGroupInfo"
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
                {{ activeGroupInfo.find(g => g.id === selectedGroup)?.name }}
              </span>
              <span class="text-gray-600 dark:text-dark-400">
                {{ t('modelPricing.discount') }}: {{ activeGroupInfo.find(g => g.id === selectedGroup)?.discount }} | {{ t('modelPricing.multiplier') }}: {{ activeGroupInfo.find(g => g.id === selectedGroup)?.multiplier }}
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
                <th v-if="showCacheCreationColumn" class="px-4 py-3 text-left font-medium text-gray-900 dark:text-white">{{ t('modelPricing.cacheCreation') }}</th>
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
                  <div class="flex flex-col gap-1">
                    <span :class="priceView === 'group' ? 'block font-semibold text-gray-900 dark:text-white' : 'block'">{{ priceView === 'group' ? formatPrice(getGroupPrice(model).input) : formatPrice(model.officialPrice.input) }}</span>
                    <span v-if="priceView === 'group'" class="block text-xs text-gray-500 dark:text-gray-400 line-through">
                      {{ formatPrice(model.officialPrice.input) }}
                    </span>
                  </div>
                </td>
                <td class="px-4 py-3 text-gray-700 dark:text-dark-300">
                  <div class="flex flex-col gap-1">
                    <span :class="priceView === 'group' ? 'block font-semibold text-gray-900 dark:text-white' : 'block'">{{ priceView === 'group' ? formatPrice(getGroupPrice(model).output) : formatPrice(model.officialPrice.output) }}</span>
                    <span v-if="priceView === 'group'" class="block text-xs text-gray-500 dark:text-gray-400 line-through">
                      {{ formatPrice(model.officialPrice.output) }}
                    </span>
                  </div>
                </td>
                <td v-if="showCacheCreationColumn" class="px-4 py-3 text-gray-700 dark:text-dark-300">
                  <div class="flex flex-col gap-1">
                    <span :class="priceView === 'group' ? 'block font-semibold text-gray-900 dark:text-white' : 'block'">{{ priceView === 'group' ? formatPrice(getGroupPrice(model).cacheCreation ?? 0) : formatPrice(model.officialPrice.cacheCreation ?? 0) }}</span>
                    <span v-if="priceView === 'group'" class="block text-xs text-gray-500 dark:text-gray-400 line-through">
                      {{ formatPrice(model.officialPrice.cacheCreation ?? 0) }}
                    </span>
                  </div>
                </td>
                <td class="px-4 py-3 text-gray-700 dark:text-dark-300">
                  <div class="flex flex-col gap-1">
                    <span :class="priceView === 'group' ? 'block font-semibold text-gray-900 dark:text-white' : 'block'">{{ priceView === 'group' ? formatPrice(getGroupPrice(model).cacheRead) : formatPrice(model.officialPrice.cacheRead) }}</span>
                    <span v-if="priceView === 'group'" class="block text-xs text-gray-500 dark:text-gray-400 line-through">
                      {{ formatPrice(model.officialPrice.cacheRead) }}
                    </span>
                  </div>
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
  // { id: 'gemini', name: 'Gemini' }
]

const selectedModel = ref('claude-code')
const priceView = ref<'group' | 'official'>('group')
const selectedGroup = ref('lite')

// Group information
const groupInfo = [
  { id: 'lite', name: 'Claude lite', discount: '80%', multiplier: '5.6' },
  // { id: 'plus', name: 'Claude Plus (精品)', discount: '85%', multiplier: '0.15' },
  // { id: 'max-cc', name: 'Claude Max (仅限CC)', discount: '80%', multiplier: '0.2' },
  // { id: 'max-external', name: 'Claude Max (外接版)', discount: '75%', multiplier: '0.25' }
]
const groupInfoCodex = [
  { id: 'lite', name: 'Codex lite', discount: '80%', multiplier: '5.6' },
]
const groupInfoByModel = {
  'claude-code': groupInfo,
  'codex': groupInfoCodex
}

const activeGroupInfo = computed(() => {
  return groupInfoByModel[selectedModel.value as keyof typeof groupInfoByModel] || groupInfo
})

type ModelPricing = {
  id: string
  groupId: string
  officialPrice: {
    input: number
    output: number
    cacheRead: number
    cacheCreation?: number
  }
  description: string
}

const showCacheCreationColumn = computed(() => selectedModel.value !== 'codex')

const formatPrice = (value: number) => `¥${value.toFixed(2)}/1M`

const getGroupPrice = (model: ModelPricing) => {
  const discount = parseFloat(activeGroupInfo.value.find((g) => g.id === selectedGroup.value)?.discount || '100') / 100

  return {
    input: model.officialPrice.input * discount,
    output: model.officialPrice.output * discount,
    cacheCreation: model.officialPrice.cacheCreation != null ? model.officialPrice.cacheCreation * discount : undefined,
    cacheRead: model.officialPrice.cacheRead * discount
  }
}

// Model pricing data (JSON structure)
const modelPricingData: Record<'claude-code' | 'codex', ModelPricing[]> = {
  'claude-code': [
    {
      id: 'claude-opus-4-8',
      groupId: 'lite',
      officialPrice: {
        input: 35.0,
        output: 175.0,
        cacheCreation: 43.75,
        cacheRead: 3.5
      },
      description: 'Claude Opus 4.8'
    },
    {
      id: 'claude-opus-4-7',
      groupId: 'lite',
      officialPrice: {
        input: 35.0,
        output: 175.0,
        cacheCreation: 43.75,
        cacheRead: 3.5
      },
      description: 'Claude Opus 4.7'
    },
    {
      id: 'claude-opus-4-6',
      groupId: 'lite',
      officialPrice: {
        input: 35.0,
        output: 175.0,
        cacheCreation: 43.75,
        cacheRead: 3.5
      },
      description: 'Claude Opus 4.6'
    },
    {
      id: 'claude-sonnet-4-6',
      groupId: 'lite',
      officialPrice: {
        input: 21.0,
        output: 105.0,
        cacheCreation: 26.25,
        cacheRead: 2.1
      },
      description: 'Claude Sonnet 4.6'
    },
    {
      id: 'claude-haiku-4-5',
      groupId: 'lite',
      officialPrice: {
        input: 7.0,
        output: 35.0,
        cacheCreation: 8.75,
        cacheRead: 0.7
      },
      description: 'Claude Haiku 4.5'
    }
  ],
  'codex': [
    {
      id: 'gpt-5.5',
      groupId: 'lite',
      officialPrice: {
        input: 35.0,
        output: 210.0,
        cacheRead: 3.5
      },
      description: 'Codex GPT-4'
    },
    {
      id: 'gpt-5.4',
      groupId: 'lite',
      officialPrice: {
        input: 17.5,
        output: 105.0,
        cacheRead: 1.75
      },
      description: 'Codex GPT-4'
    },
    {
      id: 'gpt-5.4-mini',
      groupId: 'lite',
      officialPrice: {
        input: 5.25,
        output: 31.5,
        cacheRead: 0.53
      },
      description: 'Codex GPT-4'
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
