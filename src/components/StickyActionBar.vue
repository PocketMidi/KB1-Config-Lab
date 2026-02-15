<template>
  <div class="sticky-action-bar">
    <img
      src="/load.svg"
      class="action-icon"
      title="Load"
      alt="Load"
      @click="$emit('load')"
      :class="{ disabled: !isConnected || isLoading }"
    />
    
    <img
      src="/reset.svg"
      class="action-icon"
      title="Reset"
      alt="Reset"
      @click="$emit('reset-defaults')"
      :class="{ disabled: !isConnected || isLoading }"
    />
    
    <img
      src="/save.svg"
      class="action-icon"
      title="Save"
      alt="Save"
      @click="$emit('save')"
      :class="{ disabled: !isConnected || isLoading || !hasChanges }"
    />
  </div>
</template>

<script setup lang="ts">
defineProps<{
  isConnected: boolean;
  isLoading: boolean;
  hasChanges: boolean;
}>();

defineEmits<{
  load: [];
  'reset-defaults': [];
  save: [];
}>();
</script>

<style scoped>
.sticky-action-bar {
  position: sticky;
  top: 44px; /* Height of mobile tab nav */
  z-index: 199;
  display: flex;
  gap: 1rem;
  padding: 1rem 0.75rem;
  background: var(--color-background);
  justify-content: center;
  align-items: center;
}

.action-icon {
  width: 24px;
  height: 24px;
  opacity: 0.3;
  transition: opacity 0.3s ease-in-out;
  cursor: pointer;
}

.action-icon:hover:not(.disabled) {
  opacity: 1.0;
}

.action-icon.disabled {
  opacity: 0.15;
  cursor: not-allowed;
  pointer-events: none;
}

@media (max-width: 480px) {
  .sticky-action-bar {
    padding: 0.75rem;
    gap: 0.75rem;
  }
  
  .action-icon {
    width: 22px;
    height: 22px;
  }
}

@media (min-width: 769px) {
  .sticky-action-bar {
    /* Not sticky on desktop - nav bar is not sticky */
    position: static;
    padding: 1.5rem;
  }
  
  .action-icon {
    width: 28px;
    height: 28px;
  }
}
</style>
