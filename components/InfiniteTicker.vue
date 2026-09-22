<script setup lang="ts">
withDefaults(
  defineProps<{
    items: string[]
    duration?: number // duration in seconds for one full loop
  }>(),
  {
    duration: 15
  }
)
</script>

<template>
  <!-- Container height capped to show roughly 4 items (4 * h-5 + gaps) -->
  <div class="relative h-[12.5rem] overflow-hidden">
    <div
      class="ticker-track flex flex-col gap-3"
      :style="{ animationDuration: `${duration}s` }"
    >
      <!-- Original track -->
      <div class="flex flex-col gap-3 shrink-0">
        <div
          v-for="(item, index) in items"
          :key="`orig-${index}`"
          class="flex items-center h-5 px-4 text-base font-mono"
        >
          <li>{{ item }}</li>
        </div>
      </div>

      <!-- Duplicate track for seamless loop -->
      <div class="flex flex-col gap-3 shrink-0" aria-hidden="true">
        <div
          v-for="(item, index) in items"
          :key="`dup-${index}`"
          class="flex items-center h-5 px-4 text-base font-mono"
        >
          <li>{{ item }}</li>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.ticker-track {
  animation: scroll-up linear infinite;
}

@keyframes scroll-up {
  0% {
    transform: translateY(0);
  }
  100% {
    transform: translateY(-50%);
  }
}
</style>