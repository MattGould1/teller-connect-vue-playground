<script setup lang="ts">
import { onMounted } from 'vue'
let tellerConnect: undefined

onMounted(() => {
  tellerConnect = TellerConnect.setup({
    // eslint-disable-next-line @typescript-eslint/ban-ts-comment
    // @ts-expect-error
    applicationId: import.meta.env.VITE_TELLER_APPLICATION_ID,
    // Teller's products that you would like to use, e.g. "verify"
    products: ['verify'],
    environment: 'sandbox',
    onInit: function () {
      console.log('Teller Connect has initialized')
    },
    // Part 3. Handle a successful enrollment's accessToken
    onSuccess: function (enrollment) {
      console.log('User enrolled successfully', enrollment.accessToken)
    },
    onExit: function () {
      console.log('User closed Teller Connect')
    },
  })
})

const connectApp = () => {
  // eslint-disable-next-line @typescript-eslint/ban-ts-comment
  // @ts-expect-error
  tellerConnect.open()
}
</script>

<template>
  <main>
    <button @click="connectApp">Connect to your bank</button>
  </main>
</template>
