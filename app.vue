<script setup lang="ts">
import { ref, onMounted } from 'vue';
import { initializePaddle, type Paddle } from '@paddle/paddle-js';

const paddle = ref<Paddle | undefined>(undefined);

onMounted(async () => {
  const paddleInstance = await initializePaddle({
    environment: 'sandbox',
    token: '' 
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
        priceId: ''
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
