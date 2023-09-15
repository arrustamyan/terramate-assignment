<script setup lang="ts">
const modelValue = defineModel()
const isPasswordShown = ref(false)
const togglePasswordShown = useToggle(isPasswordShown)
</script>

<template>
  <div relative>
    <Input
      v-model="modelValue"
      v-bind="$attrs"
      :type="isPasswordShown ? 'text' : 'password'"
      placeholder="************"
      minlength="32"
      :messages="{ tooShort: 'Password must be at least 32 characters long.' }"
      pr-13
    />
    <div absolute right-0 top-0 mr-6 h-12 flex items-center>
      <div v-show="!isPasswordShown" i-ph-eye h-8 w-8 @click="togglePasswordShown()" />
      <div v-show="isPasswordShown" i-ph-eye-closed h-8 w-8 @click="togglePasswordShown()" />
    </div>
  </div>
</template>
