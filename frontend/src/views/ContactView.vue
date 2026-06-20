<template>
  <div class="min-h-screen bg-primary-50 dark:bg-dark-950">
    <LandingNav />

    <main class="mx-auto max-w-6xl px-4 sm:px-6 py-8">
      <div class="rounded-[2rem] border border-gray-200 bg-white/90 p-6 sm:p-10 shadow-sm shadow-slate-900/5 backdrop-blur dark:border-dark-700/70 dark:bg-dark-900">
        <h1 class="text-4xl font-bold text-gray-900 dark:text-white lg:text-5xl">
          {{ t('contact.title') }}
        </h1>
        <p class="mt-4 max-w-2xl text-base leading-relaxed text-gray-600 dark:text-dark-300">
          {{ t('contact.description') }}
        </p>

        <div class="mt-12 grid gap-10 lg:grid-cols-[1.2fr_0.8fr]">
          <section class="space-y-8 rounded-[2rem] border border-gray-200 bg-primary-50 p-4 sm:p-6 dark:border-dark-700/70 dark:bg-dark-950">
            <div>
              <h2 class="text-2xl font-semibold text-gray-900 dark:text-white">
                {{ t('contact.wechatTitle') }}
              </h2>
              <p class="mt-3 text-sm text-gray-500 dark:text-dark-300">
                {{ t('contact.wechatDescription') }}
              </p>
            </div>
            <div class="flex justify-center rounded-[1.75rem] border border-gray-200 p-4 sm:p-6 shadow-sm dark:border-dark-700/70 dark:bg-dark-900">
              <img
                v-if="qrCodeDataUrl"
                :src="qrCodeDataUrl"
                alt="WeChat QR Code"
                class="h-72 w-full max-w-[18rem] rounded-[1.5rem] object-cover"
              />
              <div v-else class="flex h-72 w-72 items-center justify-center rounded-[1.5rem] bg-gray-100 text-sm text-gray-500 dark:bg-dark-950 dark:text-dark-500">
                {{ t('contact.qrLoading') }}
              </div>
            </div>
          </section>

          <section class="rounded-[2rem] border border-gray-200 bg-white p-6 sm:p-8 shadow-sm dark:border-dark-700/70 dark:bg-dark-900">
            <h2 class="text-2xl font-semibold text-gray-900 dark:text-white">
              {{ t('contact.emailTitle') }}
            </h2>
            <p class="mt-3 text-sm text-gray-500 dark:text-dark-300">
              {{ t('contact.emailDescription') }}
            </p>
            <div class="mt-8 rounded-[1.5rem] bg-primary-50 p-4 sm:p-6 text-lg font-semibold text-gray-900 dark:bg-dark-950 dark:text-white">
              <a class="break-all text-current" :href="`mailto:${contactEmail}`">{{ contactEmail }}</a>
            </div>
          </section>
        </div>
      </div>
    </main>

    <LandingFooter />
  </div>
</template>

<script setup lang="ts">
import { onMounted } from 'vue'
import { useI18n } from 'vue-i18n'
// import QRCode from 'qrcode'
import LandingFooter from '@/components/layout/LandingFooter.vue'
import LandingNav from '@/components/layout/LandingNav.vue'

const { t } = useI18n()
const contactEmail = 'andy@bojiangsoftware.com'
const qrCodeDataUrl = '/public/weixin.png'

onMounted(async () => {
  try {
    // qrCodeDataUrl.value = await QRCode.toDataURL('WeChat ID: sub2api_support', {
    //   width: 360,
    //   margin: 2,
    // })
  } catch (error) {
    console.error('Failed to generate QR code:', error)
  }
})
</script>
