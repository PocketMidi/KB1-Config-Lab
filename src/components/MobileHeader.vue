<template>
  <header class="mobile-header">
    <div class="header-top">
      <!-- Always show KB1 logo - centered -->
      <img src="/kb1-title.svg" alt="KB1 CONFIGURATOR" class="header-logo" />
    </div>
  </header>
</template>

<script setup lang="ts">
defineProps<{
  isConnected: boolean;
  deviceName?: string;
}>();

defineEmits<{
  connect: [];
}>();
</script>

<style scoped>
.mobile-header {
  background: #0F0F0F;
  border-bottom: none;
  position: sticky;
  top: 0;
  z-index: 100;
}

.header-top {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 1.5rem 2rem;
}

.header-logo {
  height: 60px; /* 150% of original 40px */
  width: auto;
}
</style>
