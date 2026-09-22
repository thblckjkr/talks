<script setup lang="ts">
import { computed } from 'vue'

const props = withDefaults(
  defineProps<{
    clickStage?: number
  }>(),
  {
    clickStage: 1
  }
)

const isMoved = computed(() => $clicks >= props.clickStage)
</script>

<template>
  <h1
    class="moving-title absolute origin-top-left font-bold text-4xl z-10"
    :style="{
      top: isMoved ? '0%' : '50%',
      left: isMoved ? '0%' : '50%',
      transform: isMoved
        ? 'translate(0%, 0%) scale(0.75)'
        : 'translate(-50%, -50%) scale(1)'
    }"
  >
    <slot />
  </h1>
</template>

<style scoped>
.moving-title {
  transition: all 0.6s cubic-bezier(0.4, 0, 0.2, 1);
}
</style>