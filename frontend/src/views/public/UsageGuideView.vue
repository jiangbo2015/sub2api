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
              <svg class="mt-0.5 h-5 w-5 shrink-0 text-emerald-600 dark:text-emerald-400" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.5">
                <path stroke-linecap="round" stroke-linejoin="round" d="M12 18v-5.25m0 0a6.01 6.01 0 001.5-.189m-1.5.189a6.01 6.01 0 01-1.5-.189m3.75 7.478a12.06 12.06 0 01-4.5 0m3.75 2.383a14.406 14.406 0 01-3 0M14.25 18v-.192c0-.983.658-1.823 1.508-2.316a7.5 7.5 0 10-7.517 0c.85.493 1.509 1.333 1.509 2.316V18"></path>
              </svg>
              <p class="text-sm leading-relaxed text-emerald-800 dark:text-emerald-200">
                提示：后续的 Claude Code、Codex 都依赖 Node.js 运行环境。先完成本教程，再继续各自工具配置。如果你只打算使用 CC Switch 图形客户端，可以跳过本节。
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
                <DocsCodeBlock shell="CMD / PowerShell" code="choco install nodejs-lts" />

                <p class="docs-rich-text text-sm font-medium text-gray-800 dark:text-dark-200">
                  方法三：使用
                  <a class="text-primary-600 hover:text-primary-700 dark:text-primary-400" href="https://scoop.sh/" target="_blank" rel="noopener noreferrer">Scoop</a>
                </p>
                <DocsCodeBlock shell="CMD / PowerShell" code="scoop install nodejs-lts" />
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
                <DocsCodeBlock shell="Terminal" code="brew install node" />
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
                <DocsCodeBlock shell="Terminal" :code="nvmCode" />
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
                <DocsCodeBlock shell="Terminal" :code="verifyNodeCode" />
              </div>
            </div>
          </section>

          <section id="ApiKey" class="scroll-mt-24">
            <h1 class="font-serif text-3xl font-bold text-gray-900 dark:text-white md:text-4xl">
              创建 API 密钥
            </h1>
            <p class="mt-4 text-base leading-relaxed text-gray-600 dark:text-dark-300">
              所有客户端都需要一个 API 密钥才能通过本站发起请求。整个过程大约需要 3 分钟。
            </p>

            <div class="mt-6 flex items-start gap-3 rounded-xl border border-amber-200 bg-amber-50 px-4 py-3 dark:border-amber-800/40 dark:bg-amber-900/20">
              <svg class="mt-0.5 h-5 w-5 shrink-0 text-amber-600 dark:text-amber-400" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.5">
                <path stroke-linecap="round" stroke-linejoin="round" d="M12 9v3.75m-9.303 3.376c-.866 1.5.217 3.374 1.948 3.374h14.71c1.73 0 2.813-1.874 1.948-3.374L13.949 3.378c-.866-1.5-3.032-1.5-3.898 0L2.697 16.126zM12 15.75h.007v.008H12v-.008z"></path>
              </svg>
              <p class="text-sm leading-relaxed text-amber-800 dark:text-amber-200">
                创建密钥本身不需要余额，但发起请求时会扣费。请先确认账户里有余额，或者拥有一个生效中的订阅。
              </p>
            </div>

            <div class="mt-10">
              <h2 class="border-b border-gray-200 pb-3 text-lg font-semibold text-gray-900 dark:border-dark-700 dark:text-white">
                创建步骤
              </h2>
              <div class="mt-5 space-y-4">
                <ol class="docs-rich-text list-decimal space-y-2 pl-5 text-sm leading-relaxed text-gray-600 dark:text-dark-300">
                  <li>
                    进入
                    <router-link to="/keys" class="text-primary-600 hover:text-primary-700 dark:text-primary-400">API 密钥管理</router-link>
                    页面。页面顶部会显示 API 端点，也就是下面各客户端要填的服务地址。
                  </li>
                  <li>点击右上角的「创建密钥」按钮。</li>
                  <li>填写<strong class="font-medium text-gray-800 dark:text-dark-200">名称</strong>，起一个方便自己区分用途的名字即可。</li>
                  <li>选择<strong class="font-medium text-gray-800 dark:text-dark-200">分组</strong>，这是最关键的一步，详见下方说明。</li>
                  <li>点击「创建」，然后在列表中点击复制按钮拿到完整密钥。</li>
                </ol>
              </div>
            </div>

            <div class="mt-10">
              <h2 class="border-b border-gray-200 pb-3 text-lg font-semibold text-gray-900 dark:border-dark-700 dark:text-white">
                关于分组
              </h2>
              <div class="mt-5 space-y-4">
                <p class="text-sm leading-relaxed text-gray-600 dark:text-dark-300">
                  分组决定了这个密钥能调用哪些模型、按什么价格计费，也决定了它能配合哪些客户端使用。请根据你要使用的工具来选择对应平台的分组。
                </p>
                <ul class="list-disc space-y-2 pl-5 text-sm leading-relaxed text-gray-600 dark:text-dark-300">
                  <li>下拉列表里只会显示你有权使用的分组。</li>
                  <li>专属分组需要管理员手动开通后才会出现。</li>
                  <li>订阅制分组需要先购买对应的订阅套餐才会出现。</li>
                  <li>如果列表为空，请联系管理员确认权限。</li>
                </ul>
              </div>
            </div>

            <div class="mt-10">
              <h2 class="border-b border-gray-200 pb-3 text-lg font-semibold text-gray-900 dark:border-dark-700 dark:text-white">
                可选限制
              </h2>
              <div class="mt-5 space-y-4">
                <p class="text-sm leading-relaxed text-gray-600 dark:text-dark-300">
                  以下选项默认全部关闭，日常使用可以跳过。适合在把密钥配置到自动化脚本或共享环境时用来控制风险。
                </p>
                <div class="overflow-hidden rounded-xl border border-gray-200 dark:border-dark-700">
                  <table class="w-full text-sm">
                    <thead class="bg-gray-100 dark:bg-dark-800">
                      <tr>
                        <th class="px-4 py-2.5 text-left font-medium text-gray-700 dark:text-dark-200">选项</th>
                        <th class="px-4 py-2.5 text-left font-medium text-gray-700 dark:text-dark-200">说明</th>
                      </tr>
                    </thead>
                    <tbody class="divide-y divide-gray-200 dark:divide-dark-700">
                      <tr v-for="option in keyOptions" :key="option.name">
                        <td class="whitespace-nowrap px-4 py-2.5 font-medium text-gray-800 dark:text-dark-200">{{ option.name }}</td>
                        <td class="px-4 py-2.5 leading-relaxed text-gray-600 dark:text-dark-300">{{ option.desc }}</td>
                      </tr>
                    </tbody>
                  </table>
                </div>
              </div>
            </div>

            <div class="mt-6 flex items-start gap-3 rounded-xl border border-blue-200 bg-blue-50 px-4 py-3 dark:border-blue-800/40 dark:bg-blue-900/20">
              <svg class="mt-0.5 h-5 w-5 shrink-0 text-blue-600 dark:text-blue-400" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.5">
                <path stroke-linecap="round" stroke-linejoin="round" d="M11.25 11.25l.041-.02a.75.75 0 011.063.852l-.708 2.836a.75.75 0 001.063.853l.041-.021M21 12a9 9 0 11-18 0 9 9 0 0118 0zm-9-3.75h.008v.008H12V8.25z"></path>
              </svg>
              <p class="text-sm leading-relaxed text-blue-800 dark:text-blue-200">
                密钥在列表中是打码显示的，但完整内容可以随时通过复制按钮重新获取，不是只显示一次。不过请像对待密码一样保管它——任何拿到密钥的人都能消耗你的余额。
              </p>
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
              <svg class="mt-0.5 h-5 w-5 shrink-0 text-blue-600 dark:text-blue-400" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.5">
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
                  中创建的密钥。config.toml 的内容请放在文件开头部分。
                </p>
                <DocsCodeBlock path="~/.codex/config.toml" :code="codexConfigCode" />
                <DocsCodeBlock path="~/.codex/auth.json" :code="codexAuthCode" />
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
                <DocsCodeBlock shell="Terminal" code="codex" />
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
              页面点击「导入到 CCS」，即可将本站 API 密钥快速导入到 CC Switch，无需手动编辑任何配置文件。
            </p>

            <div class="mt-10">
              <h2 class="border-b border-gray-200 pb-3 text-lg font-semibold text-gray-900 dark:border-dark-700 dark:text-white">
                导入步骤
              </h2>
              <div class="mt-5 space-y-4">
                <ol class="docs-rich-text list-decimal space-y-2 pl-5 text-sm leading-relaxed text-gray-600 dark:text-dark-300">
                  <li>
                    先安装 CC Switch 客户端，详见
                    <a class="text-primary-600 hover:text-primary-700 dark:text-primary-400" href="https://ccswitch.io/zh/" target="_blank" rel="noopener noreferrer">官方文档</a>。
                  </li>
                  <li>回到 API 密钥页面，在目标密钥所在行点击「导入到 CCS」。</li>
                  <li>浏览器会唤起 CC Switch 客户端并自动填入服务地址和密钥，确认后即可使用。</li>
                </ol>
                <p class="text-sm leading-relaxed text-gray-600 dark:text-dark-300">
                  导入时会根据密钥所属分组的平台，自动写入对应的客户端配置，并开启用量显示（每 30 分钟自动刷新一次余额）。
                </p>
                <div class="overflow-hidden rounded-xl border border-gray-200 dark:border-dark-700">
                  <table class="w-full text-sm">
                    <thead class="bg-gray-100 dark:bg-dark-800">
                      <tr>
                        <th class="px-4 py-2.5 text-left font-medium text-gray-700 dark:text-dark-200">分组平台</th>
                        <th class="px-4 py-2.5 text-left font-medium text-gray-700 dark:text-dark-200">导入为</th>
                      </tr>
                    </thead>
                    <tbody class="divide-y divide-gray-200 dark:divide-dark-700">
                      <tr v-for="row in ccSwitchMapping" :key="row.platform">
                        <td class="whitespace-nowrap px-4 py-2.5 font-medium text-gray-800 dark:text-dark-200">{{ row.platform }}</td>
                        <td class="px-4 py-2.5 leading-relaxed text-gray-600 dark:text-dark-300">{{ row.target }}</td>
                      </tr>
                    </tbody>
                  </table>
                </div>
              </div>
            </div>

            <div class="mt-6 flex items-start gap-3 rounded-xl border border-violet-200 bg-violet-50 px-4 py-3 dark:border-violet-800/40 dark:bg-violet-900/20">
              <svg class="mt-0.5 h-5 w-5 shrink-0 text-violet-600 dark:text-violet-400" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.5">
                <path stroke-linecap="round" stroke-linejoin="round" d="M12 6.75a5.25 5.25 0 015.25 5.25v.75h.75a1.5 1.5 0 011.5 1.5v3.75a1.5 1.5 0 01-1.5 1.5H6a1.5 1.5 0 01-1.5-1.5v-3.75a1.5 1.5 0 011.5-1.5h.75v-.75A5.25 5.25 0 0112 6.75zm2.25 6v-.75a2.25 2.25 0 10-4.5 0v.75h4.5z"></path>
              </svg>
              <p class="text-sm leading-relaxed text-violet-800 dark:text-violet-200">
                如果点击后没有反应，或提示「CC-Switch 未安装或协议处理程序未注册」，说明电脑上没有安装 CC Switch，或浏览器没有注册 ccswitch:// 协议。请先安装客户端；如果仍然不行，改用手动复制密钥的方式配置即可。
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
                <DocsCodeBlock shell="macOS / Linux" :code="claudeUnixCode" />
                <DocsCodeBlock shell="Windows CMD" :code="claudeCmdCode" />
                <DocsCodeBlock shell="PowerShell" :code="claudePowershellCode" />
                <p class="text-sm leading-relaxed text-gray-500 dark:text-dark-400">
                  直接在终端中运行只对当前窗口生效。想要永久生效，请写入上面提到的 shell 配置文件；Windows 用户可以写入系统环境变量。
                </p>
              </div>
            </div>

            <div class="mt-10">
              <h2 class="border-b border-gray-200 pb-3 text-lg font-semibold text-gray-900 dark:border-dark-700 dark:text-white">
                VSCode 配置
              </h2>
              <div class="mt-5 space-y-4">
                <p class="text-sm leading-relaxed text-gray-600 dark:text-dark-300">
                  如果使用 VSCode 版 Claude Code，可在 ~/.claude/settings.json 中写入以下配置（Windows 路径为 %userprofile%\.claude\settings.json）：
                </p>
                <DocsCodeBlock path="~/.claude/settings.json" :code="claudeVscodeCode" />
              </div>
            </div>
          </section>

          <section id="GeminiCli" class="scroll-mt-24">
            <h1 class="font-serif text-3xl font-bold text-gray-900 dark:text-white md:text-4xl">
              Gemini CLI 配置教程
            </h1>
            <p class="mt-4 text-base leading-relaxed text-gray-600 dark:text-dark-300">
              通过环境变量将 Gemini CLI 指向本站 API 网关。需要使用 Gemini 类分组的密钥。
            </p>

            <div class="mt-10">
              <h2 class="border-b border-gray-200 pb-3 text-lg font-semibold text-gray-900 dark:border-dark-700 dark:text-white">
                环境变量配置
              </h2>
              <div class="mt-5 space-y-4">
                <DocsCodeBlock shell="macOS / Linux" :code="geminiUnixCode" />
                <DocsCodeBlock shell="PowerShell" :code="geminiPowershellCode" />
                <p class="text-sm leading-relaxed text-gray-500 dark:text-dark-400">
                  GEMINI_MODEL 可以按需修改。如果你的分组有 Gemini 3 权限，可以填 gemini-3-pro-preview。
                </p>
              </div>
            </div>
          </section>

          <section id="OpenCode" class="scroll-mt-24">
            <h1 class="font-serif text-3xl font-bold text-gray-900 dark:text-white md:text-4xl">
              OpenCode 配置教程
            </h1>
            <p class="mt-4 text-base leading-relaxed text-gray-600 dark:text-dark-300">
              OpenCode 支持本站的多种分组平台，配置写在一个 JSON 文件中。
            </p>

            <div class="mt-10">
              <h2 class="border-b border-gray-200 pb-3 text-lg font-semibold text-gray-900 dark:border-dark-700 dark:text-white">
                配置文件
              </h2>
              <div class="mt-5 space-y-4">
                <p class="docs-rich-text text-sm leading-relaxed text-gray-600 dark:text-dark-300">
                  编辑 ~/.config/opencode/opencode.json（也支持 opencode.jsonc），文件不存在需要手动创建。由于不同分组平台的 provider 配置差异较大，建议直接在
                  <router-link to="/keys" class="text-primary-600 hover:text-primary-700 dark:text-primary-400">API 密钥管理</router-link>
                  页面点击密钥所在行的「使用密钥」，切换到 OpenCode 标签页复制已经填好服务地址和密钥的完整配置，避免手动编写出错。
                </p>
              </div>
            </div>
          </section>

          <section id="Manage" class="scroll-mt-24">
            <h1 class="font-serif text-3xl font-bold text-gray-900 dark:text-white md:text-4xl">
              密钥日常管理
            </h1>
            <p class="mt-4 text-base leading-relaxed text-gray-600 dark:text-dark-300">
              在 API 密钥列表中，每个密钥都支持以下操作。列表同时会显示今日用量、近 30 天用量、额度使用进度和速率限制使用情况。
            </p>

            <div class="mt-10">
              <div class="overflow-hidden rounded-xl border border-gray-200 dark:border-dark-700">
                <table class="w-full text-sm">
                  <thead class="bg-gray-100 dark:bg-dark-800">
                    <tr>
                      <th class="px-4 py-2.5 text-left font-medium text-gray-700 dark:text-dark-200">操作</th>
                      <th class="px-4 py-2.5 text-left font-medium text-gray-700 dark:text-dark-200">说明</th>
                    </tr>
                  </thead>
                  <tbody class="divide-y divide-gray-200 dark:divide-dark-700">
                    <tr v-for="action in keyActions" :key="action.name">
                      <td class="whitespace-nowrap px-4 py-2.5 font-medium text-gray-800 dark:text-dark-200">{{ action.name }}</td>
                      <td class="px-4 py-2.5 leading-relaxed text-gray-600 dark:text-dark-300">{{ action.desc }}</td>
                    </tr>
                  </tbody>
                </table>
              </div>
              <p class="mt-4 text-sm leading-relaxed text-gray-500 dark:text-dark-400">
                密钥状态包括：活跃、已停用、额度耗尽、已过期。可以通过顶部的搜索框和筛选器快速定位。
              </p>
            </div>
          </section>

          <section id="Faq" class="scroll-mt-24">
            <h1 class="font-serif text-3xl font-bold text-gray-900 dark:text-white md:text-4xl">
              常见问题
            </h1>

            <div class="mt-8 space-y-6">
              <div v-for="item in faqItems" :key="item.q">
                <h2 class="text-base font-semibold text-gray-900 dark:text-white">{{ item.q }}</h2>
                <p class="mt-2 text-sm leading-relaxed text-gray-600 dark:text-dark-300">{{ item.a }}</p>
              </div>
            </div>
          </section>
        </main>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { computed, onMounted, onUnmounted, ref } from 'vue'
import { useI18n } from 'vue-i18n'
import PublicHeader from '@/components/common/PublicHeader.vue'
import DocsCodeBlock from '@/components/docs/DocsCodeBlock.vue'
import { useAppStore } from '@/stores/app'

const { t } = useI18n()
const appStore = useAppStore()
const currentAnchor = ref('Nodejs')

const API_KEY_PLACEHOLDER = 'YOUR_API_KEY'

// Prefer the configured public endpoint; fall back to wherever the site is served from.
const baseUrl = computed(() =>
  (appStore.apiBaseUrl || window.location.origin).replace(/\/+$/, '')
)

const navItems = [
  { id: 'Nodejs', label: 'Node.js 环境安装教程' },
  { id: 'ApiKey', label: '创建 API 密钥' },
  { id: 'Codex', label: 'Codex 配置教程' },
  { id: 'CCSwitch', label: 'CC Switch 配置教程' },
  { id: 'ClaudeCode', label: 'Claude Code 配置教程' },
  { id: 'GeminiCli', label: 'Gemini CLI 配置教程' },
  { id: 'OpenCode', label: 'OpenCode 配置教程' },
  { id: 'Manage', label: '密钥日常管理' },
  { id: 'Faq', label: '常见问题' }
]

const keyOptions = [
  { name: '自定义密钥', desc: '自己指定密钥内容而非随机生成。至少 16 个字符，只能包含字母、数字、下划线和连字符。' },
  { name: 'IP 限制', desc: '设置 IP 白名单或黑名单，每行一个 IP 或 CIDR 网段。适合固定办公网络或服务器部署。' },
  { name: '额度限制', desc: '限制这个密钥最多能消费多少美元，填 0 或留空表示不限制。额度用完后状态变为「额度耗尽」，可随时重置。' },
  { name: '速率限制', desc: '分别设置 5 小时、日、7 天的消费上限（单位美元），填 0 表示不限制。' },
  { name: '密钥有效期', desc: '可选 7 天、30 天、90 天或自定义过期时间。不开启则永久有效。' }
]

const ccSwitchMapping = [
  { platform: 'Claude 类', target: 'Claude Code' },
  { platform: 'Codex / OpenAI 类', target: 'Codex，同时写入默认模型' },
  { platform: 'Gemini 类', target: 'Gemini CLI' },
  { platform: 'Antigravity 类', target: '弹窗让你选择 Claude Code 或 Gemini CLI' }
]

const keyActions = [
  { name: '使用密钥', desc: '随时查看已填好服务地址和密钥的客户端配置内容。' },
  { name: '复制', desc: '复制完整密钥。列表中显示的是打码版本，复制得到的是完整内容。' },
  { name: '编辑', desc: '修改名称、额度、速率限制、有效期、IP 限制等。' },
  { name: '启用 / 禁用', desc: '临时停用某个密钥，不影响其他密钥。' },
  { name: '删除', desc: '永久删除，无法撤销，删除后立刻失效。' },
  { name: '切换分组', desc: '直接点击列表中的分组名称即可更换。' },
  { name: '导入到 CCS', desc: '一键把配置导入 CC Switch 客户端，部分站点未开放此功能。' }
]

const faqItems = [
  {
    q: '创建密钥时下拉列表里没有可选的分组？',
    a: '说明你当前没有任何可用分组。可能是你需要的分组为专属分组，需要联系管理员开通；也可能是订阅制分组，需要先购买对应套餐。'
  },
  {
    q: '点击「使用密钥」提示「请先分配分组」？',
    a: '说明这个密钥当前没有绑定分组。回到列表，点击该密钥所在行的分组列，选择一个分组即可。'
  },
  {
    q: '请求报错提示余额不足？',
    a: '请前往充值或订阅页面补充余额、购买套餐。如果没有看到该页面，说明本站未开放自助充值，请联系管理员。'
  },
  {
    q: '请求报错提示无可用账号或服务暂时不可用？',
    a: '这通常是上游服务临时波动导致的，请稍后重试。如果持续出现，请联系管理员。'
  },
  {
    q: '能不能一个密钥同时用于 Claude Code 和 Codex？',
    a: '不能。一个密钥只能绑定一个分组，而分组对应特定的上游平台。需要同时使用多个平台时，请分别创建多个密钥。'
  },
  {
    q: '提示 node 或 npm 不是内部或外部命令？',
    a: '说明 Node.js 没有安装成功，或者安装后没有重启终端。请重新打开一个终端窗口再试，仍然不行就回到本页开头重新安装。'
  },
  {
    q: '忘记保存密钥了怎么办？',
    a: '不需要担心，随时回到 API 密钥页面点击复制按钮即可重新获取完整密钥。'
  },
  {
    q: '密钥泄露了怎么办？',
    a: '立即在列表中禁用或删除该密钥，然后创建一个新的。删除后该密钥会立刻失效。'
  }
]

const nvmCode = `curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash
nvm install --lts`

const verifyNodeCode = `node -v
npm -v`

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

const codexAuthCode = `{
  "OPENAI_API_KEY": "${API_KEY_PLACEHOLDER}"
}`

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

const geminiUnixCode = computed(() => `export GOOGLE_GEMINI_BASE_URL="${baseUrl.value}"
export GEMINI_API_KEY="${API_KEY_PLACEHOLDER}"
export GEMINI_MODEL="gemini-2.0-flash"`)

const geminiPowershellCode = computed(() => `$env:GOOGLE_GEMINI_BASE_URL="${baseUrl.value}"
$env:GEMINI_API_KEY="${API_KEY_PLACEHOLDER}"
$env:GEMINI_MODEL="gemini-2.0-flash"`)

const scrollTo = (id: string) => {
  const el = document.getElementById(id)
  if (el) {
    el.scrollIntoView({ behavior: 'smooth', block: 'start' })
    currentAnchor.value = id
  }
}

let observer: IntersectionObserver | null = null

onMounted(() => {
  void appStore.fetchPublicSettings()

  observer = new IntersectionObserver(
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
    if (el) observer?.observe(el)
  })
})

onUnmounted(() => {
  observer?.disconnect()
})
</script>
