<script setup lang="ts">
const modelValue = defineModel()
</script>

<template>
  <Input
    v-model="modelValue"
    v-bind="$attrs"
    type="email"
    placeholder="email@example.com"
    :messages="{ typeMismatch: 'Please enter a valid email address.' }"
  />
</template>
