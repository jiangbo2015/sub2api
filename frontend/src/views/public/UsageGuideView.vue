<template>
  <div class="min-h-screen bg-gray-50 text-gray-900 dark:bg-dark-950 dark:text-white">
    <PublicHeader :login-destination="'/login'" :login-text="t('home.login')" />

    <div class="mx-auto max-w-6xl px-6 py-8">
      <div class="mb-6 flex gap-2 overflow-x-auto pb-1 lg:hidden">
        <button
          v-for="item in navItems"
          :key="item.id"
          type="button"
          class="shrink-0 rounded-full px-4 py-2 text-sm font-medium transition-colors"
          :class="currentAnchor === item.id
            ? 'bg-primary-100 text-primary-800 dark:bg-primary-900/40 dark:text-primary-200'
            : 'bg-white text-gray-600 dark:bg-dark-800 dark:text-dark-300'"
          @click="scrollTo(item.id)"
        >
          {{ item.label }}
        </button>
      </div>

      <div class="flex gap-10">
        <aside class="hidden w-56 shrink-0 lg:block">
          <nav class="sticky top-24">
            <p class="mb-3 text-sm font-semibold text-gray-900 dark:text-white">快速上手</p>
            <ul class="space-y-1">
              <li v-for="item in navItems" :key="item.id">
                <a
                  :href="`#${item.id}`"
                  class="block rounded-lg px-3 py-2 text-sm transition-colors"
                  :class="currentAnchor === item.id
                    ? 'bg-primary-200 font-medium text-primary-800 dark:bg-primary-900/30 dark:text-primary-200'
                    : 'text-gray-600 hover:bg-white/60 hover:text-primary-700 dark:text-dark-300 dark:hover:bg-dark-800 dark:hover:text-primary-300'"
                >
                  {{ item.label }}
                </a>
              </li>
            </ul>
          </nav>
        </aside>

        <main class="min-w-0 flex-1 space-y-16 pb-16">
          <section id="Nodejs" class="scroll-mt-24">
            <h1 class="font-serif text-3xl font-bold text-gray-900 dark:text-white md:text-4xl">
              Node.js 环境安装教程
            </h1>
            <p class="mt-4 text-base leading-relaxed text-gray-600 dark:text-dark-300">
              在 Windows、macOS、Linux 安装 Node.js LTS，并验证 node/npm 命令可用。
            </p>

            <div class="mt-6 flex items-start gap-3 rounded-xl border border-emerald-200 bg-emerald-50 px-4 py-3 dark:border-emerald-800/40 dark:bg-emerald-900/20">
              <svg class="mt-0.5 h-5 w-5 text-emerald-600 dark:text-emerald-400" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.5">
                <path stroke-linecap="round" stroke-linejoin="round" d="M12 18v-5.25m0 0a6.01 6.01 0 001.5-.189m-1.5.189a6.01 6.01 0 01-1.5-.189m3.75 7.478a12.06 12.06 0 01-4.5 0m3.75 2.383a14.406 14.406 0 01-3 0M14.25 18v-.192c0-.983.658-1.823 1.508-2.316a7.5 7.5 0 10-7.517 0c.85.493 1.509 1.333 1.509 2.316V18"></path>
              </svg>
              <p class="text-sm leading-relaxed text-emerald-800 dark:text-emerald-200">
                提示：后续的 Claude Code、Codex 都依赖 Node.js 运行环境。先完成本教程，再继续各自工具配置。
              </p>
            </div>

            <div class="mt-10">
              <h2 class="border-b border-gray-200 pb-3 text-lg font-semibold text-gray-900 dark:border-dark-700 dark:text-white">
                Windows
              </h2>
              <div class="mt-5 space-y-4">
                <p class="docs-rich-text text-sm leading-relaxed text-gray-600 dark:text-dark-300">
                  方法一：官方下载（推荐）—— 前往
                  <a class="text-primary-600 hover:text-primary-700 dark:text-primary-400" href="https://nodejs.org/zh-cn" target="_blank" rel="noopener noreferrer">Node.js 官网</a>
                  下载 LTS 安装包并安装。
                </p>
                <p class="docs-rich-text text-sm font-medium text-gray-800 dark:text-dark-200">
                  方法二：使用
                  <a class="text-primary-600 hover:text-primary-700 dark:text-primary-400" href="https://chocolatey.org/" target="_blank" rel="noopener noreferrer">Chocolatey</a>
                </p>
                <div class="overflow-hidden rounded-xl border border-gray-800 bg-gray-900">
                  <div class="flex items-center justify-between border-b border-gray-700 px-4 py-2.5">
                    <span class="text-xs font-medium text-gray-400">CMD / PowerShell</span>
                    <button type="button" class="rounded-md px-2.5 py-1 text-xs font-medium text-gray-300 transition-colors hover:bg-gray-700 hover:text-white">
                      复制
                    </button>
                  </div>
                  <pre class="overflow-x-auto p-4 text-sm leading-relaxed text-gray-100"><code>choco install nodejs-lts</code></pre>
                </div>

                <p class="docs-rich-text text-sm font-medium text-gray-800 dark:text-dark-200">
                  方法三：使用
                  <a class="text-primary-600 hover:text-primary-700 dark:text-primary-400" href="https://scoop.sh/" target="_blank" rel="noopener noreferrer">Scoop</a>
                </p>
                <div class="overflow-hidden rounded-xl border border-gray-800 bg-gray-900">
                  <div class="flex items-center justify-between border-b border-gray-700 px-4 py-2.5">
                    <span class="text-xs font-medium text-gray-400">CMD / PowerShell</span>
                    <button type="button" class="rounded-md px-2.5 py-1 text-xs font-medium text-gray-300 transition-colors hover:bg-gray-700 hover:text-white">
                      复制
                    </button>
                  </div>
                  <pre class="overflow-x-auto p-4 text-sm leading-relaxed text-gray-100"><code>scoop install nodejs-lts</code></pre>
                </div>
              </div>
            </div>

            <div class="mt-10">
              <h2 class="border-b border-gray-200 pb-3 text-lg font-semibold text-gray-900 dark:border-dark-700 dark:text-white">
                macOS
              </h2>
              <div class="mt-5 space-y-4">
                <p class="docs-rich-text text-sm leading-relaxed text-gray-600 dark:text-dark-300">
                  方法一：官方下载（推荐）—— 前往
                  <a class="text-primary-600 hover:text-primary-700 dark:text-primary-400" href="https://nodejs.org/zh-cn" target="_blank" rel="noopener noreferrer">Node.js 官网</a>
                  下载 macOS 安装包。
                </p>
                <p class="docs-rich-text text-sm font-medium text-gray-800 dark:text-dark-200">
                  方法二：使用
                  <a class="text-primary-600 hover:text-primary-700 dark:text-primary-400" href="https://brew.sh/" target="_blank" rel="noopener noreferrer">Homebrew</a>
                </p>
                <div class="overflow-hidden rounded-xl border border-gray-800 bg-gray-900">
                  <div class="flex items-center justify-between border-b border-gray-700 px-4 py-2.5">
                    <span class="text-xs font-medium text-gray-400">Terminal</span>
                    <button type="button" class="rounded-md px-2.5 py-1 text-xs font-medium text-gray-300 transition-colors hover:bg-gray-700 hover:text-white">
                      复制
                    </button>
                  </div>
                  <pre class="overflow-x-auto p-4 text-sm leading-relaxed text-gray-100"><code>brew install node</code></pre>
                </div>
              </div>
            </div>

            <div class="mt-10">
              <h2 class="border-b border-gray-200 pb-3 text-lg font-semibold text-gray-900 dark:border-dark-700 dark:text-white">
                Linux
              </h2>
              <div class="mt-5 space-y-4">
                <p class="docs-rich-text text-sm leading-relaxed text-gray-600 dark:text-dark-300">
                  推荐通过
                  <a class="text-primary-600 hover:text-primary-700 dark:text-primary-400" href="https://github.com/nvm-sh/nvm" target="_blank" rel="noopener noreferrer">nvm</a>
                  安装 LTS 版本，便于多版本管理：
                </p>
                <div class="overflow-hidden rounded-xl border border-gray-800 bg-gray-900">
                  <div class="flex items-center justify-between border-b border-gray-700 px-4 py-2.5">
                    <span class="text-xs font-medium text-gray-400">Terminal</span>
                    <button type="button" class="rounded-md px-2.5 py-1 text-xs font-medium text-gray-300 transition-colors hover:bg-gray-700 hover:text-white">
                      复制
                    </button>
                  </div>
                  <pre class="overflow-x-auto p-4 text-sm leading-relaxed text-gray-100"><code>curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash
nvm install --lts</code></pre>
                </div>
              </div>
            </div>

            <div class="mt-10">
              <h2 class="border-b border-gray-200 pb-3 text-lg font-semibold text-gray-900 dark:border-dark-700 dark:text-white">
                验证安装
              </h2>
              <div class="mt-5 space-y-4">
                <p class="text-sm leading-relaxed text-gray-600 dark:text-dark-300">
                  安装完成后，在终端执行以下命令，确认 node 和 npm 可用：
                </p>
                <div class="overflow-hidden rounded-xl border border-gray-800 bg-gray-900">
                  <div class="flex items-center justify-between border-b border-gray-700 px-4 py-2.5">
                    <span class="text-xs font-medium text-gray-400">Terminal</span>
                    <button type="button" class="rounded-md px-2.5 py-1 text-xs font-medium text-gray-300 transition-colors hover:bg-gray-700 hover:text-white">
                      复制
                    </button>
                  </div>
                  <pre class="overflow-x-auto p-4 text-sm leading-relaxed text-gray-100"><code>node -v
npm -v</code></pre>
                </div>
              </div>
            </div>
          </section>

          <section id="Codex" class="scroll-mt-24">
            <h1 class="font-serif text-3xl font-bold text-gray-900 dark:text-white md:text-4xl">
              Codex 配置教程
            </h1>
            <p class="mt-4 text-base leading-relaxed text-gray-600 dark:text-dark-300">
              将 API 密钥写入 Codex CLI 配置目录，即可通过本站中转访问 OpenAI Codex 模型。
            </p>

            <div class="mt-6 flex items-start gap-3 rounded-xl border border-blue-200 bg-blue-50 px-4 py-3 dark:border-blue-800/40 dark:bg-blue-900/20">
              <svg class="mt-0.5 h-5 w-5 text-blue-600 dark:text-blue-400" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.5">
                <path stroke-linecap="round" stroke-linejoin="round" d="M11.25 11.25l.041-.02a.75.75 0 011.063.852l-.708 2.836a.75.75 0 001.063.853l.041-.021M21 12a9 9 0 11-18 0 9 9 0 0118 0zm-9-3.75h.008v.008H12V8.25z"></path>
              </svg>
              <p class="text-sm leading-relaxed text-blue-800 dark:text-blue-200">
                请确保配置目录存在。macOS/Linux 可运行 mkdir -p ~/.codex；Windows 按 Win+R 输入 %userprofile%\.codex 打开目录。
              </p>
            </div>

            <div class="mt-10">
              <h2 class="border-b border-gray-200 pb-3 text-lg font-semibold text-gray-900 dark:border-dark-700 dark:text-white">
                配置文件
              </h2>
              <div class="mt-5 space-y-4">
                <p class="docs-rich-text text-sm leading-relaxed text-gray-600 dark:text-dark-300">
                  在 ~/.codex 目录下创建 config.toml 和 auth.json，将 YOUR_API_KEY 替换为
                  <router-link to="/keys" class="text-primary-600 hover:text-primary-700 dark:text-primary-400">API 密钥管理</router-link>
                  中创建的密钥。
                </p>
                <div class="overflow-hidden rounded-xl border border-gray-800 bg-gray-900">
                  <div class="flex items-center justify-between border-b border-gray-700 px-4 py-2.5">
                    <span class="text-xs font-medium text-gray-400">~/.codex/config.toml</span>
                    <button type="button" class="rounded-md px-2.5 py-1 text-xs font-medium text-gray-300 transition-colors hover:bg-gray-700 hover:text-white">
                      复制
                    </button>
                  </div>
                  <pre class="overflow-x-auto p-4 text-sm leading-relaxed text-gray-100"><code>model_provider = "OpenAI"
model = "gpt-5.5"
review_model = "gpt-5.5"
model_reasoning_effort = "xhigh"
disable_response_storage = true
network_access = "enabled"
windows_wsl_setup_acknowledged = true

[model_providers.OpenAI]
name = "OpenAI"
base_url = "https://pineai.net"
wire_api = "responses"
requires_openai_auth = true

[features]
goals = true</code></pre>
                </div>

                <div class="overflow-hidden rounded-xl border border-gray-800 bg-gray-900">
                  <div class="flex items-center justify-between border-b border-gray-700 px-4 py-2.5">
                    <span class="text-xs font-medium text-gray-400">~/.codex/auth.json</span>
                    <button type="button" class="rounded-md px-2.5 py-1 text-xs font-medium text-gray-300 transition-colors hover:bg-gray-700 hover:text-white">
                      复制
                    </button>
                  </div>
                  <pre class="overflow-x-auto p-4 text-sm leading-relaxed text-gray-100"><code>{
  "OPENAI_API_KEY": "YOUR_API_KEY"
}</code></pre>
                </div>
              </div>
            </div>

            <div class="mt-10">
              <h2 class="border-b border-gray-200 pb-3 text-lg font-semibold text-gray-900 dark:border-dark-700 dark:text-white">
                验证配置
              </h2>
              <div class="mt-5 space-y-4">
                <p class="text-sm leading-relaxed text-gray-600 dark:text-dark-300">
                  配置完成后，在终端运行 codex 命令测试连接是否正常。
                </p>
                <div class="overflow-hidden rounded-xl border border-gray-800 bg-gray-900">
                  <div class="flex items-center justify-between border-b border-gray-700 px-4 py-2.5">
                    <span class="text-xs font-medium text-gray-400">Terminal</span>
                    <button type="button" class="rounded-md px-2.5 py-1 text-xs font-medium text-gray-300 transition-colors hover:bg-gray-700 hover:text-white">
                      复制
                    </button>
                  </div>
                  <pre class="overflow-x-auto p-4 text-sm leading-relaxed text-gray-100"><code>codex</code></pre>
                </div>
              </div>
            </div>
          </section>

          <section id="CCSwitch" class="scroll-mt-24">
            <h1 class="font-serif text-3xl font-bold text-gray-900 dark:text-white md:text-4xl">
              CC Switch 配置教程
            </h1>
            <p class="mt-4 text-base leading-relaxed text-gray-600 dark:text-dark-300">
              在
              <router-link to="/keys" class="text-primary-600 hover:text-primary-700 dark:text-primary-400">API 密钥管理</router-link>
              页面点击“导入到CCS”，即可将本站 API 密钥快速导入到 CC Switch。
            </p>

            <div class="mt-6 flex items-start gap-3 rounded-xl border border-violet-200 bg-violet-50 px-4 py-3 dark:border-violet-800/40 dark:bg-violet-900/20">
              <svg class="mt-0.5 h-5 w-5 text-violet-600 dark:text-violet-400" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.5">
                <path stroke-linecap="round" stroke-linejoin="round" d="M12 6.75a5.25 5.25 0 015.25 5.25v.75h.75a1.5 1.5 0 011.5 1.5v3.75a1.5 1.5 0 01-1.5 1.5H6a1.5 1.5 0 01-1.5-1.5v-3.75a1.5 1.5 0 011.5-1.5h.75v-.75A5.25 5.25 0 0112 6.75zm2.25 6v-.75a2.25 2.25 0 10-4.5 0v.75h4.5z"></path>
              </svg>
              <p class="text-sm leading-relaxed text-violet-800 dark:text-violet-200">
                详细使用说明可参考官方文档：
                <a class="text-primary-600 hover:text-primary-700 dark:text-primary-400" href="https://ccswitch.io/zh/" target="_blank" rel="noopener noreferrer">CC Switch</a>
              </p>
            </div>
          </section>

          <section id="ClaudeCode" class="scroll-mt-24">
            <h1 class="font-serif text-3xl font-bold text-gray-900 dark:text-white md:text-4xl">
              Claude Code 配置教程
            </h1>
            <p class="mt-4 text-base leading-relaxed text-gray-600 dark:text-dark-300">
              通过环境变量或 VSCode 配置文件，将 Claude Code 指向本站 API 网关。
            </p>

            <div class="mt-10">
              <h2 class="border-b border-gray-200 pb-3 text-lg font-semibold text-gray-900 dark:border-dark-700 dark:text-white">
                环境变量配置
              </h2>
              <div class="mt-5 space-y-4">
                <p class="docs-rich-text text-sm leading-relaxed text-gray-600 dark:text-dark-300">
                  将以下环境变量添加到终端配置文件（~/.bashrc、~/.zshrc）或直接在终端中运行。将 YOUR_API_KEY 替换为
                  <router-link to="/keys" class="text-primary-600 hover:text-primary-700 dark:text-primary-400">API 密钥管理</router-link>
                  中创建的密钥。
                </p>
                <div class="overflow-hidden rounded-xl border border-gray-800 bg-gray-900">
                  <div class="flex items-center justify-between border-b border-gray-700 px-4 py-2.5">
                    <span class="text-xs font-medium text-gray-400">macOS / Linux</span>
                    <button type="button" class="rounded-md px-2.5 py-1 text-xs font-medium text-gray-300 transition-colors hover:bg-gray-700 hover:text-white">
                      复制
                    </button>
                  </div>
                  <pre class="overflow-x-auto p-4 text-sm leading-relaxed text-gray-100"><code>export ANTHROPIC_BASE_URL="https://pineai.net"
export ANTHROPIC_AUTH_TOKEN="YOUR_API_KEY"
export CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC=1</code></pre>
                </div>

                <div class="overflow-hidden rounded-xl border border-gray-800 bg-gray-900">
                  <div class="flex items-center justify-between border-b border-gray-700 px-4 py-2.5">
                    <span class="text-xs font-medium text-gray-400">Windows CMD</span>
                    <button type="button" class="rounded-md px-2.5 py-1 text-xs font-medium text-gray-300 transition-colors hover:bg-gray-700 hover:text-white">
                      复制
                    </button>
                  </div>
                  <pre class="overflow-x-auto p-4 text-sm leading-relaxed text-gray-100"><code>set ANTHROPIC_BASE_URL=https://pineai.net
set ANTHROPIC_AUTH_TOKEN=YOUR_API_KEY
set CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC=1</code></pre>
                </div>

                <div class="overflow-hidden rounded-xl border border-gray-800 bg-gray-900">
                  <div class="flex items-center justify-between border-b border-gray-700 px-4 py-2.5">
                    <span class="text-xs font-medium text-gray-400">PowerShell</span>
                    <button type="button" class="rounded-md px-2.5 py-1 text-xs font-medium text-gray-300 transition-colors hover:bg-gray-700 hover:text-white">
                      复制
                    </button>
                  </div>
                  <pre class="overflow-x-auto p-4 text-sm leading-relaxed text-gray-100"><code>$env:ANTHROPIC_BASE_URL="https://pineai.net"
$env:ANTHROPIC_AUTH_TOKEN="YOUR_API_KEY"
$env:CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC=1</code></pre>
                </div>
              </div>
            </div>

            <div class="mt-10">
              <h2 class="border-b border-gray-200 pb-3 text-lg font-semibold text-gray-900 dark:border-dark-700 dark:text-white">
                VSCode 配置
              </h2>
              <div class="mt-5 space-y-4">
                <p class="text-sm leading-relaxed text-gray-600 dark:text-dark-300">
                  如果使用 VSCode 版 Claude Code，可在 ~/.claude/settings.json 中写入以下配置：
                </p>
                <div class="overflow-hidden rounded-xl border border-gray-800 bg-gray-900">
                  <div class="flex items-center justify-between border-b border-gray-700 px-4 py-2.5">
                    <span class="text-xs font-medium text-gray-400">~/.claude/settings.json</span>
                    <button type="button" class="rounded-md px-2.5 py-1 text-xs font-medium text-gray-300 transition-colors hover:bg-gray-700 hover:text-white">
                      复制
                    </button>
                  </div>
                  <pre class="overflow-x-auto p-4 text-sm leading-relaxed text-gray-100"><code>{
  "env": {
    "ANTHROPIC_BASE_URL": "https://pineai.net",
    "ANTHROPIC_AUTH_TOKEN": "YOUR_API_KEY",
    "CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC": "1",
    "CLAUDE_CODE_ATTRIBUTION_HEADER": "0"
  }
}</code></pre>
                </div>
              </div>
            </div>
          </section>
        </main>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { onMounted, ref } from 'vue'
import { useI18n } from 'vue-i18n'
import PublicHeader from '@/components/common/PublicHeader.vue'

const { t } = useI18n()
const currentAnchor = ref('Nodejs')

const navItems = [
  { id: 'Nodejs', label: 'Node.js 环境安装教程' },
  { id: 'Codex', label: 'Codex 配置教程' },
  { id: 'CCSwitch', label: 'CC Switch 配置教程' },
  { id: 'ClaudeCode', label: 'Claude Code 配置教程' }
]

const scrollTo = (id: string) => {
  const el = document.getElementById(id)
  if (el) {
    el.scrollIntoView({ behavior: 'smooth', block: 'start' })
    currentAnchor.value = id
  }
}

onMounted(() => {
  const observer = new IntersectionObserver(
    (entries) => {
      const visible = entries
        .filter((entry) => entry.isIntersecting)
        .sort((a, b) => b.intersectionRatio - a.intersectionRatio)[0]
      if (visible?.target?.id) {
        currentAnchor.value = visible.target.id
      }
    },
    { rootMargin: '-20% 0px -55% 0px', threshold: [0.2, 0.4, 0.6] }
  )

  navItems.forEach(({ id }) => {
    const el = document.getElementById(id)
    if (el) observer.observe(el)
  })

  return () => observer.disconnect()
})
</script>
