<template>
  <CurrencyConverter />
</template>

<script>

import CurrencyConverter from "@/components/CurrencyConverter.vue";

export default {
  name: 'App',
  components: {
    CurrencyConverter
  }
}
</script>

<style>
#app {
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
