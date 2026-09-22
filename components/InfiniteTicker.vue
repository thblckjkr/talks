<script setup lang="ts">
withDefaults(
  defineProps<{
    items: string[]
    duration?: number // duration in seconds for one full loop
  }>(),
  {
    duration: 20
  }
)
</script>

<template>
  <div class="ticker-container w-full overflow-hidden whitespace-nowrap py-2">
    <div
      class="ticker-track inline-flex gap-8"
      :style="{ animationDuration: `${duration}s` }"
    >
      <!-- Original track -->
      <div class="flex gap-8 shrink-0 items-center">
        <span
          v-for="(item, index) in items"
          :key="`orig-${index}`"
          class=""
        >
          {{ item }}
        </span>
      </div>

      <!-- Duplicate track for seamless loop -->
      <div class="flex gap-8 shrink-0 items-center" aria-hidden="true">
        <span
          v-for="(item, index) in items"
          :key="`dup-${index}`"
          class=""
        >
          {{ item }}
        </span>
      </div>
    </div>
  </div>
</template>

<style scoped>
.ticker-track {
  animation: scroll-left linear infinite;
}

@keyframes scroll-left {
  0% {
    transform: translateX(0);
  }
  100% {
    transform: translateX(-50%);
  }
}
</style>