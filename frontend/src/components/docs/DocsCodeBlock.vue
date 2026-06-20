<template>
  <div class="overflow-hidden rounded-xl border border-gray-800 bg-gray-900" :class="blockClass">
    <div class="flex items-center justify-between border-b border-gray-700 px-4 py-2.5">
      <span class="text-xs font-medium text-gray-400">{{ label }}</span>
      <button
        type="button"
        class="rounded-md px-2.5 py-1 text-xs font-medium text-gray-300 transition-colors hover:bg-gray-700 hover:text-white"
        @click="handleCopy"
      >
        {{ copied ? t('docs.copied') : t('docs.copy') }}
      </button>
    </div>
    <pre class="overflow-x-auto p-4 text-sm leading-relaxed text-gray-100"><code>{{ code }}</code></pre>
  </div>
</template>

<script setup lang="ts">
import { computed, ref } from 'vue'
import { useI18n } from 'vue-i18n'
import { useClipboard } from '@/composables/useClipboard'

const props = defineProps<{
  code: string
  shell?: string
  path?: string
  blockClass?: string
}>()

const { t } = useI18n()
const { copyToClipboard } = useClipboard()
const copied = ref(false)

const label = computed(() => props.path || props.shell || 'Code')

async function handleCopy() {
  const success = await copyToClipboard(props.code)
  if (!success) return
  copied.value = true
  window.setTimeout(() => {
    copied.value = false
  }, 2000)
}
</script>
