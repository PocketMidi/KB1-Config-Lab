<template>
  <div class="settings-leverpush" :class="`lever-${lever}`">
    <div class="title">
      <h2>{{ title }} {{ lever }}</h2>
      <div v-if="isValidCC">
        <span>MIDI CC</span>
        <span>{{ model.ccNumber }}</span>
      </div>
    </div>

    <div class="inputs">
      <div class="group">
        <label :for="`push-ccNumber-${lever}`">Parameter</label>
        <select :id="`push-ccNumber-${lever}`" v-model.number="model.ccNumber">
          <option v-for="opt in ccOptions" :key="opt.value" :value="opt.value">{{ opt.label }}</option>
        </select>
      </div>

      <div class="group">
        <label :for="`push-functionMode-${lever}`">Function Mode</label>
        <select :id="`push-functionMode-${lever}`" v-model.number="model.functionMode">
          <option v-for="opt in functionModes" :key="opt.value" :value="opt.value">{{ opt.label }}</option>
        </select>
      </div>

      <div class="group">
        <label :for="`push-maxCCValue-${lever}`">CC Max</label>
        <input type="number" :id="`push-maxCCValue-${lever}`" v-model.number="model.maxCCValue" />
      </div>

      <div class="group">
        <label :for="`push-minCCValue-${lever}`">CC Min</label>
        <input type="number" :id="`push-minCCValue-${lever}`" v-model.number="model.minCCValue" />
      </div>

      <div class="group">
        <label :for="`push-onsetType-${lever}`">Attack Type</label>
        <select :id="`push-onsetType-${lever}`" v-model.number="model.onsetType">
          <option v-for="opt in interpolations" :key="opt.value" :value="opt.value">{{ opt.label }}</option>
        </select>
      </div>

      <div class="group">
        <label :for="`push-onsetTime-${lever}`">Attack Time</label>
        <div class="number-with-unit">
          <input type="number" :id="`push-onsetTime-${lever}`" v-model.number="model.onsetTime" />
          <span>ms</span>
        </div>
      </div>

      <div class="group">
        <label :for="`push-offsetType-${lever}`">Decay Type</label>
        <select :id="`push-offsetType-${lever}`" v-model.number="model.offsetType">
          <option v-for="opt in interpolations" :key="opt.value" :value="opt.value">{{ opt.label }}</option>
        </select>
      </div>

      <div class="group">
        <label :for="`push-offsetTime-${lever}`">Decay Time</label>
        <div class="number-with-unit">
          <input type="number" :id="`push-offsetTime-${lever}`" v-model.number="model.offsetTime" />
          <span>ms</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { computed } from 'vue'

type LeverPushModel = {
  ccNumber: number
  minCCValue: number
  maxCCValue: number
  functionMode: number
  onsetTime: number
  offsetTime: number
  onsetType: number
  offsetType: number
}

const props = defineProps<{
  title?: string
  lever: number
  modelValue: LeverPushModel
  ccOptions: { value: number, label: string }[]
  functionModes: { value: number, label: string }[]
  interpolations: { value: number, label: string }[]
}>()

const emit = defineEmits<{
  (e: 'update:modelValue', v: LeverPushModel): void
}>()

const model = computed({
  get: () => props.modelValue,
  set: v => emit('update:modelValue', v)
})

const isValidCC = computed(() => model.value.ccNumber >= 0 && model.value.ccNumber <= 127)
</script>

<style scoped>
.settings-leverpush {
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

.title div {
  display: flex;
  align-items: center;
  gap: var(--kb1-spacing-sm, 0.5rem);
  background: var(--title-cc-bg, rgba(59, 130, 246, 0.1));
  padding: var(--title-cc-padding, 0.5rem 1rem);
  border-radius: var(--title-cc-radius, 6px);
  font-size: var(--kb1-font-size-sm, 0.875rem);
}

.title div span:first-child {
  color: var(--color-text-muted);
}

.title div span:last-child {
  color: var(--title-cc-color, #3b82f6);
  font-weight: 600;
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

.group select,
.group input[type="number"] {
  padding: var(--input-padding, 0.75rem);
  background: var(--input-bg, var(--color-background));
  border: var(--input-border, 1px solid var(--color-border));
  border-radius: var(--input-radius, 6px);
  color: var(--input-color, var(--color-text));
  font-size: 1rem;
}

.group select:focus,
.group input[type="number"]:focus {
  outline: none;
  border: var(--input-border-focus, 1px solid #3b82f6);
}

.number-with-unit {
  display: flex;
  align-items: center;
  gap: var(--kb1-spacing-sm, 0.5rem);
}

.number-with-unit input {
  flex: 1;
}

.number-with-unit span {
  color: var(--color-text-muted);
  font-size: var(--kb1-font-size-sm, 0.875rem);
  min-width: 2rem;
}
</style>