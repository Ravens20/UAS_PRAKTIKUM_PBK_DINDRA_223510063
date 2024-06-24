// src/pages/Home.vue
<template>
  <div class="page">
    <WeatherWidget />
  </div>
</template>

<script>
import WeatherWidget from '../components/WeatherWidget.vue';

export default {
  name: 'HomePage',
  components: {
    WeatherWidget
  }
};
</script>

<style>
.page {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  flex-direction: column;
}
</style>
