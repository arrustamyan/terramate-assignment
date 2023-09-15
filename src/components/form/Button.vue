<script setup lang="ts">
const props = defineProps<{
  isLoading?: boolean
  disabled?: boolean
}>()
</script>

<template>
  <button v-bind="$attrs" :disabled="disabled || props.isLoading" m-3 h-12 w-96 flex items-center justify-center text-lg btn>
    <slot />
    <div v-show="props.isLoading" i-ph-spinner ml-3 h-8 w-8 animate-spin />
  </button>
</template>
