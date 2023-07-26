<script setup>
import { RouterView } from "vue-router"
import SiteNavigation from "./components/SiteNavigation.vue";
</script>
<template>
  <div class="flex flex-col min-h-screen bg-weather-primary">
    <SiteNavigation/>
    <RouterView/>
  </div>
</template>