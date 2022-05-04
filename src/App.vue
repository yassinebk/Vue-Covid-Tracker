<script setup lang="ts">
import { RouterLink, RouterView } from "vue-router";
import Header from "@/components/Header.vue";
</script>

<template>

  <Header />
  <div class="container mx-auto font-[Poppins]">
    <RouterView />
  </div>
</template>

<style scoped>
html {
  font-family: Poppins, Helvetica, sans-serif;
}
</style>
