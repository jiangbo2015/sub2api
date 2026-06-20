<template>
  <div class="min-h-screen bg-primary-100 dark:bg-dark-900">
    <LandingNav />

    <div class="mx-auto max-w-6xl px-6 py-8">
      <div class="mb-6 flex gap-2 overflow-x-auto pb-1 lg:hidden">
        <button
          v-for="item in navItems"
          :key="item.id"
          type="button"
          class="shrink-0 rounded-full px-4 py-2 text-sm font-medium transition-colors"
          :class="activeSection === item.id
            ? 'bg-primary-100 text-primary-800 dark:bg-primary-900/40 dark:text-primary-200'
            : 'bg-white text-gray-600 dark:bg-dark-800 dark:text-dark-300'"
          @click="navigateToSection(item.id)"
        >
          {{ item.label }}
        </button>
      </div>

      <div class="flex gap-10">
        <aside class="hidden w-56 shrink-0 lg:block">
          <nav class="sticky top-24">
            <p class="mb-3 text-sm font-semibold text-gray-900 dark:text-white">{{ t('docs.quickStart') }}</p>
            <ul class="space-y-1">
              <li v-for="item in navItems" :key="item.id">
                <a
                  :href="`#${item.id}`"
                  class="block rounded-lg px-3 py-2 text-sm transition-colors"
                  :class="activeSection === item.id
                    ? 'bg-[#F5E6D8] font-medium text-primary-800 dark:bg-primary-900/30 dark:text-primary-200'
                    : 'text-gray-600 hover:bg-white/60 hover:text-primary-700 dark:text-dark-300 dark:hover:bg-dark-800 dark:hover:text-primary-300'"
                  @click.prevent="navigateToSection(item.id)"
                >
                  {{ item.label }}
                </a>
              </li>
            </ul>
          </nav>
        </aside>

        <main class="min-w-0 flex-1 space-y-16 pb-16">
          <section :id="SECTION_IDS.nodejs" class="scroll-mt-24">
            <h1 class="font-serif text-3xl font-bold text-gray-900 dark:text-white md:text-4xl">
              {{ t('docs.nodejs.title') }}
            </h1>
            <p class="mt-4 text-base leading-relaxed text-gray-600 dark:text-dark-300">
              {{ t('docs.nodejs.description') }}
            </p>

            <div class="mt-6 flex items-start gap-3 rounded-xl border border-emerald-200 bg-emerald-50 px-4 py-3 dark:border-emerald-800/40 dark:bg-emerald-900/20">
              <span class="material-symbols-outlined mt-0.5 text-[20px] text-emerald-600 dark:text-emerald-400">lightbulb</span>
              <p class="text-sm leading-relaxed text-emerald-800 dark:text-emerald-200">{{ t('docs.nodejs.tip') }}</p>
            </div>

            <div class="mt-10">
              <h2 class="border-b border-gray-200 pb-3 text-lg font-semibold text-gray-900 dark:border-dark-700 dark:text-white">{{ t('docs.nodejs.windows') }}</h2>
              <div class="mt-5 space-y-4">
                <p class="text-sm leading-relaxed text-gray-600 dark:text-dark-300">{{ t('docs.nodejs.windowsMethod1') }}</p>
                <p class="text-sm font-medium text-gray-800 dark:text-dark-200">{{ t('docs.nodejs.windowsMethod2') }}</p>
                <DocsCodeBlock shell="CMD / PowerShell" :code="windowsChocoCode" />
                <p class="text-sm font-medium text-gray-800 dark:text-dark-200">{{ t('docs.nodejs.windowsMethod3') }}</p>
                <DocsCodeBlock shell="CMD / PowerShell" :code="windowsScoopCode" />
              </div>
            </div>

            <div class="mt-10">
              <h2 class="border-b border-gray-200 pb-3 text-lg font-semibold text-gray-900 dark:border-dark-700 dark:text-white">{{ t('docs.nodejs.macos') }}</h2>
              <div class="mt-5 space-y-4">
                <p class="text-sm leading-relaxed text-gray-600 dark:text-dark-300">{{ t('docs.nodejs.macosMethod1') }}</p>
                <p class="text-sm font-medium text-gray-800 dark:text-dark-200">{{ t('docs.nodejs.macosMethod2') }}</p>
                <DocsCodeBlock shell="Terminal" :code="macosBrewCode" />
              </div>
            </div>

            <div class="mt-10">
              <h2 class="border-b border-gray-200 pb-3 text-lg font-semibold text-gray-900 dark:border-dark-700 dark:text-white">{{ t('docs.nodejs.linux') }}</h2>
              <div class="mt-5 space-y-4">
                <p class="text-sm leading-relaxed text-gray-600 dark:text-dark-300">{{ t('docs.nodejs.linuxMethod1') }}</p>
                <DocsCodeBlock shell="Terminal" :code="linuxNvmCode" />
              </div>
            </div>

            <div class="mt-10">
              <h2 class="border-b border-gray-200 pb-3 text-lg font-semibold text-gray-900 dark:border-dark-700 dark:text-white">{{ t('docs.nodejs.verify') }}</h2>
              <div class="mt-5 space-y-4">
                <p class="text-sm leading-relaxed text-gray-600 dark:text-dark-300">{{ t('docs.nodejs.verifyDescription') }}</p>
                <DocsCodeBlock shell="Terminal" :code="verifyCode" />
              </div>
            </div>
          </section>

          <section :id="SECTION_IDS.codex" class="scroll-mt-24">
            <h1 class="font-serif text-3xl font-bold text-gray-900 dark:text-white md:text-4xl">
              {{ t('docs.codex.title') }}
            </h1>
            <p class="mt-4 text-base leading-relaxed text-gray-600 dark:text-dark-300">
              {{ t('docs.codex.description') }}
            </p>

            <div class="mt-6 flex items-start gap-3 rounded-xl border border-blue-200 bg-blue-50 px-4 py-3 dark:border-blue-800/40 dark:bg-blue-900/20">
              <span class="material-symbols-outlined mt-0.5 text-[20px] text-blue-600 dark:text-blue-400">info</span>
              <p class="text-sm leading-relaxed text-blue-800 dark:text-blue-200">{{ t('docs.codex.note') }}</p>
            </div>

            <div class="mt-10">
              <h2 class="border-b border-gray-200 pb-3 text-lg font-semibold text-gray-900 dark:border-dark-700 dark:text-white">{{ t('docs.codex.configTitle') }}</h2>
              <div class="mt-5 space-y-4">
                <p class="text-sm leading-relaxed text-gray-600 dark:text-dark-300">{{ t('docs.codex.configDescription') }}</p>
                <DocsCodeBlock :path="codexConfigPath" :code="codexConfigCode" />
                <DocsCodeBlock :path="codexAuthPath" :code="codexAuthCode" />
              </div>
            </div>

            <div class="mt-10">
              <h2 class="border-b border-gray-200 pb-3 text-lg font-semibold text-gray-900 dark:border-dark-700 dark:text-white">{{ t('docs.codex.verifyTitle') }}</h2>
              <div class="mt-5 space-y-4">
                <p class="text-sm leading-relaxed text-gray-600 dark:text-dark-300">{{ t('docs.codex.verifyDescription') }}</p>
                <DocsCodeBlock shell="Terminal" :code="codexVerifyCode" />
              </div>
            </div>
          </section>

          <section :id="SECTION_IDS.claudeCode" class="scroll-mt-24">
            <h1 class="font-serif text-3xl font-bold text-gray-900 dark:text-white md:text-4xl">
              {{ t('docs.claudeCode.title') }}
            </h1>
            <p class="mt-4 text-base leading-relaxed text-gray-600 dark:text-dark-300">
              {{ t('docs.claudeCode.description') }}
            </p>

            <div class="mt-10">
              <h2 class="border-b border-gray-200 pb-3 text-lg font-semibold text-gray-900 dark:border-dark-700 dark:text-white">{{ t('docs.claudeCode.envTitle') }}</h2>
              <div class="mt-5 space-y-4">
                <p class="text-sm leading-relaxed text-gray-600 dark:text-dark-300">{{ t('docs.claudeCode.envDescription') }}</p>
                <DocsCodeBlock shell="macOS / Linux" :code="claudeUnixCode" />
                <DocsCodeBlock shell="Windows CMD" :code="claudeCmdCode" />
                <DocsCodeBlock shell="PowerShell" :code="claudePowershellCode" />
              </div>
            </div>

            <div class="mt-10">
              <h2 class="border-b border-gray-200 pb-3 text-lg font-semibold text-gray-900 dark:border-dark-700 dark:text-white">{{ t('docs.claudeCode.vscodeTitle') }}</h2>
              <div class="mt-5 space-y-4">
                <p class="text-sm leading-relaxed text-gray-600 dark:text-dark-300">{{ t('docs.claudeCode.vscodeDescription') }}</p>
                <DocsCodeBlock path="~/.claude/settings.json" :code="claudeVscodeCode" />
              </div>
            </div>
          </section>

          <section :id="SECTION_IDS.geminiCli" class="scroll-mt-24">
            <h1 class="font-serif text-3xl font-bold text-gray-900 dark:text-white md:text-4xl">
              {{ t('docs.geminiCli.title') }}
            </h1>
            <p class="mt-4 text-base leading-relaxed text-gray-600 dark:text-dark-300">
              {{ t('docs.geminiCli.description') }}
            </p>

            <div class="mt-10">
              <h2 class="border-b border-gray-200 pb-3 text-lg font-semibold text-gray-900 dark:border-dark-700 dark:text-white">{{ t('docs.geminiCli.envTitle') }}</h2>
              <div class="mt-5 space-y-4">
                <p class="text-sm leading-relaxed text-gray-600 dark:text-dark-300">{{ t('docs.geminiCli.envDescription') }}</p>
                <DocsCodeBlock shell="macOS / Linux" :code="geminiUnixCode" />
                <DocsCodeBlock shell="Windows CMD" :code="geminiCmdCode" />
                <DocsCodeBlock shell="PowerShell" :code="geminiPowershellCode" />
              </div>
            </div>

            <div class="mt-6 flex items-start gap-3 rounded-xl border border-blue-200 bg-blue-50 px-4 py-3 dark:border-blue-800/40 dark:bg-blue-900/20">
              <span class="material-symbols-outlined mt-0.5 text-[20px] text-blue-600 dark:text-blue-400">info</span>
              <p class="text-sm leading-relaxed text-blue-800 dark:text-blue-200">{{ t('docs.geminiCli.note') }}</p>
            </div>
          </section>
        </main>
      </div>
    </div>

    <LandingFooter />
  </div>
</template>

<script setup lang="ts">
import { computed, onMounted, onUnmounted, ref, watch } from 'vue'
import { useRoute, useRouter } from 'vue-router'
import { useI18n } from 'vue-i18n'
import LandingNav from '@/components/layout/LandingNav.vue'
import LandingFooter from '@/components/layout/LandingFooter.vue'
import DocsCodeBlock from '@/components/docs/DocsCodeBlock.vue'

const SECTION_IDS = {
  nodejs: 'Nodejs',
  codex: 'Codex',
  claudeCode: 'ClaudeCode',
  geminiCli: 'GeminiCLI',
} as const

type SectionId = typeof SECTION_IDS[keyof typeof SECTION_IDS]

const { t } = useI18n()
const route = useRoute()
const router = useRouter()

const API_KEY_PLACEHOLDER = 'YOUR_API_KEY'
const baseUrl = computed(() => window.location.origin.replace(/\/+$/, ''))
const geminiBaseUrl = computed(() => `${baseUrl.value}/v1beta`)

const navItems = computed(() => [
  { id: SECTION_IDS.nodejs, label: t('docs.nav.nodejs') },
  { id: SECTION_IDS.codex, label: t('docs.nav.codex') },
  { id: SECTION_IDS.claudeCode, label: t('docs.nav.claudeCode') },
  { id: SECTION_IDS.geminiCli, label: t('docs.nav.geminiCli') },
])

const activeSection = ref<SectionId>(SECTION_IDS.nodejs)

const windowsChocoCode = 'choco install nodejs-lts'
const windowsScoopCode = 'scoop install nodejs-lts'
const macosBrewCode = 'brew install node'
const linuxNvmCode = `curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash
nvm install --lts`
const verifyCode = `node -v
npm -v`

const codexConfigPath = '~/.codex/config.toml'
const codexAuthPath = '~/.codex/auth.json'
const codexConfigCode = computed(() => `model_provider = "OpenAI"
model = "gpt-5.5"
review_model = "gpt-5.5"
model_reasoning_effort = "xhigh"
disable_response_storage = true
network_access = "enabled"
windows_wsl_setup_acknowledged = true

[model_providers.OpenAI]
name = "OpenAI"
base_url = "${baseUrl.value}"
wire_api = "responses"
requires_openai_auth = true

[features]
goals = true`)
const codexAuthCode = computed(() => `{
  "OPENAI_API_KEY": "${API_KEY_PLACEHOLDER}"
}`)
const codexVerifyCode = 'codex'

const claudeUnixCode = computed(() => `export ANTHROPIC_BASE_URL="${baseUrl.value}"
export ANTHROPIC_AUTH_TOKEN="${API_KEY_PLACEHOLDER}"
export CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC=1`)
const claudeCmdCode = computed(() => `set ANTHROPIC_BASE_URL=${baseUrl.value}
set ANTHROPIC_AUTH_TOKEN=${API_KEY_PLACEHOLDER}
set CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC=1`)
const claudePowershellCode = computed(() => `$env:ANTHROPIC_BASE_URL="${baseUrl.value}"
$env:ANTHROPIC_AUTH_TOKEN="${API_KEY_PLACEHOLDER}"
$env:CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC=1`)
const claudeVscodeCode = computed(() => `{
  "env": {
    "ANTHROPIC_BASE_URL": "${baseUrl.value}",
    "ANTHROPIC_AUTH_TOKEN": "${API_KEY_PLACEHOLDER}",
    "CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC": "1",
    "CLAUDE_CODE_ATTRIBUTION_HEADER": "0"
  }
}`)

const geminiModel = 'gemini-2.0-flash'
const geminiUnixCode = computed(() => `export GOOGLE_GEMINI_BASE_URL="${geminiBaseUrl.value}"
export GEMINI_API_KEY="${API_KEY_PLACEHOLDER}"
export GEMINI_MODEL="${geminiModel}"`)
const geminiCmdCode = computed(() => `set GOOGLE_GEMINI_BASE_URL=${geminiBaseUrl.value}
set GEMINI_API_KEY=${API_KEY_PLACEHOLDER}
set GEMINI_MODEL=${geminiModel}`)
const geminiPowershellCode = computed(() => `$env:GOOGLE_GEMINI_BASE_URL="${geminiBaseUrl.value}"
$env:GEMINI_API_KEY="${API_KEY_PLACEHOLDER}"
$env:GEMINI_MODEL="${geminiModel}"`)

function isValidSectionId(value: string): value is SectionId {
  return Object.values(SECTION_IDS).includes(value as SectionId)
}

function scrollToSection(id: SectionId) {
  document.getElementById(id)?.scrollIntoView({ behavior: 'smooth' })
}

function navigateToSection(id: SectionId) {
  activeSection.value = id
  router.replace({ path: '/docs', hash: `#${id}` })
  scrollToSection(id)
}

function syncFromHash() {
  const hash = route.hash.replace(/^#/, '')
  if (isValidSectionId(hash)) {
    activeSection.value = hash
    requestAnimationFrame(() => scrollToSection(hash))
  }
}

let observer: IntersectionObserver | null = null

function setupSectionObserver() {
  observer?.disconnect()
  observer = new IntersectionObserver(
    (entries) => {
      const visible = entries
        .filter((entry) => entry.isIntersecting)
        .sort((a, b) => b.intersectionRatio - a.intersectionRatio)
      if (!visible.length) return
      const id = visible[0].target.id
      if (isValidSectionId(id)) {
        activeSection.value = id
      }
    },
    { rootMargin: '-20% 0px -60% 0px', threshold: [0, 0.25, 0.5, 1] },
  )

  Object.values(SECTION_IDS).forEach((id) => {
    const element = document.getElementById(id)
    if (element) observer?.observe(element)
  })
}

watch(() => route.hash, () => {
  syncFromHash()
})

onMounted(() => {
  if (!route.hash) {
    router.replace({ path: '/docs', hash: `#${SECTION_IDS.nodejs}` })
  } else {
    syncFromHash()
  }
  setupSectionObserver()
})

onUnmounted(() => {
  observer?.disconnect()
})
</script>
