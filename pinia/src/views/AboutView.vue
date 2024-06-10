<script setup>
import { useCounterStore } from '@/stores/counter';

const counterStore = useCounterStore();
</script>

<template>
  <div class="about">
    <h1>This is an about page</h1>
  </div>
  <button class="counter-button">{{ counterStore.count }}</button>
</template>

<style>
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
  .counter-button{
    font-size: 50px;
  }
}
</style>
