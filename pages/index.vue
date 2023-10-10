<template>
  <div>
    <h1>Home page</h1>
    <ClientOnly>
      <h2>Temperature today</h2>
      <ChartTemperature />
      <h2>Rain today</h2>
      <ChartRain />
      <h2>Wind Speed today</h2>
      <ChartWindSpeed />
    </ClientOnly>
  </div>
</template>
<script setup lang="ts">
</script>