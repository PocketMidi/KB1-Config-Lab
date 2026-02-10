<template>
  <div class="settings-scale">
    <div class="title">
      <h2>{{ title }}</h2>
    </div>

    <div class="inputs">
      <div class="group">
        <label for="scale-scaletype">Scale</label>
        <select id="scale-scaletype" v-model.number="model.scaleType">
          <option v-for="opt in scales" :key="opt.value" :value="opt.value">{{ opt.label }}</option>
        </select>
      </div>

      <div class="group">
        <label for="scale-rootnote">Root Note</label>
        <select id="scale-rootnote" v-model.number="model.rootNote">
          <option v-for="opt in rootNotes" :key="opt.value" :value="opt.value">{{ opt.label }}</option>
        </select>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { computed } from 'vue'

type ScaleModel = {
  scaleType: number
  rootNote: number
}

const props = defineProps<{
  title?: string
  modelValue: ScaleModel
  scales: { value: number, label: string }[]
  rootNotes: { value: number, label: string }[]
}>()

const emit = defineEmits<{
  (e: 'update:modelValue', v: ScaleModel): void
}>()

const model = computed({
  get: () => props.modelValue,
  set: v => emit('update:modelValue', v)
})
</script>

<style scoped>
.settings-scale {
  display: flex;
  flex-direction: column;
  gap: var(--settings-panel-gap, 1rem);
}

.title {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding-bottom: var(--kb1-spacing-md, 1rem);
  border-bottom: 1px solid var(--color-border);
}

.title h2 {
  margin: 0;
  font-size: var(--title-font-size, 1.25rem);
  font-weight: var(--title-font-weight, 600);
  color: var(--title-color, var(--color-text));
}

.inputs {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: var(--settings-panel-gap, 1rem);
}

.group {
  display: flex;
  flex-direction: column;
  gap: var(--kb1-spacing-sm, 0.5rem);
}

.group label {
  font-size: var(--label-font-size, 0.875rem);
  font-weight: var(--label-font-weight, 500);
  color: var(--label-color, var(--color-text));
}

.group select {
  padding: var(--input-padding, 0.75rem);
  background: var(--input-bg, var(--color-background));
  border: var(--input-border, 1px solid var(--color-border));
  border-radius: var(--input-radius, 6px);
  color: var(--input-color, var(--color-text));
  font-size: 1rem;
}

.group select:focus {
  outline: none;
  border: var(--input-border-focus, 1px solid #3b82f6);
}
</style>