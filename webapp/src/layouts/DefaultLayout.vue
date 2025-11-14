<template>
  <div>
    <slot name="header" />

    <!-- Main content -->
    <main class="mb-16">
      <slot />
    </main>

    <!-- Footer -->
    <Footer />
  </div>
</template>

<script setup lang="ts">
import Footer from '../components/layout/Footer.vue'
</script>
