<script setup lang="ts">

// import { useRouteQuery } from '@vueuse/router'

// const text = useRouteQuery('text')

import { useTitle, useUrlSearchParams } from '@vueuse/core'
import { useQRCode } from './composable/useQrCode'
import { computed } from 'vue';

const params = useUrlSearchParams('history')


const text = computed(() => params.text as string)
useTitle(text)

// `qrcode` will be a ref of data URL
const qrcode = useQRCode(text, {
    errorCorrectionLevel: 'H',
    margin: 3,
    type: 'svg',
})



</script>

<template>
    <main class="bg-slate-600 h-screen w-screen p-8">
        <section class="max-w-lg md:max-w-5xl mx-auto grid md:grid-cols-2 gap-6">

            <textarea v-model="params.text" resize="none" class="w-full aspect-square rounded-md p-6" />

            <div v-show="params.text" v-html="qrcode" class="w-full aspect-square rounded-md overflow-hidden" />
        </section>

    </main>
</template>
