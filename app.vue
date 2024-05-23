<script setup lang="ts">
import { ref, onMounted } from 'vue';
import { initializePaddle, type Paddle } from '@paddle/paddle-js';

const paddle = ref<Paddle | undefined>(undefined);

onMounted(async () => {
  const paddleInstance = await initializePaddle({
    environment: 'sandbox',
    token: 'live_086c73ae87243fb1d1413cc85a4' 
  });
  if (paddleInstance) {
    paddle.value = paddleInstance;
  }

  console.info('paddle', paddle.value?.Environment?.get());

});


const openCheckout = () => {
  paddle?.value?.Checkout.open({
    settings: {
      displayMode: 'overlay',
      theme: 'dark'
    },
    items: [
      {
        quantity: 1,
        priceId: 'pri_01hq52466a4tqfc4bsz0f62f87'
      }
    ]
  })
};

</script>

<template>
  <div>
    <button @click="openCheckout">
        <span class="inline-block">Pay Button</span>
    </button>
  </div>
</template>
