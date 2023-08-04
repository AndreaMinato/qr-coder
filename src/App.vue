<script setup lang="ts">

// import { useRouteQuery } from '@vueuse/router'

// const text = useRouteQuery('text')

import { useUrlSearchParams } from '@vueuse/core'
import { useQRCode } from './composable/useQrCode'
import { computed } from 'vue';

const params = useUrlSearchParams('history')


const text = computed(()=> params.text as string)

// `qrcode` will be a ref of data URL
const qrcode = useQRCode(text, {

    errorCorrectionLevel: 'H',
  margin: 3,
      type: 'svg',

})



</script>

<template>
    <main class="grid grid-cols-2 gap-2">



                <textarea v-model="params.text" resize="none" class="w-full aspect-square"/>



                <div v-show="params.text" v-html="qrcode" class="w-full aspect-square"  />

    </main>
</template>
