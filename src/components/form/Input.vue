<script setup lang="ts">
const props = defineProps<{
  messages?: Partial<{ [key in keyof ValidityState]: string }>
}>()

const VALIDATION_MESSAGES: { [key in keyof ValidityState]: string } = {
  badInput: 'Bad input',
  customError: 'Error.',
  patternMismatch: 'The value does not match required format.',
  rangeOverflow: 'Bad input.',
  rangeUnderflow: 'Bad input.',
  stepMismatch: 'Bad input.',
  tooLong: 'The value is too long.',
  tooShort: 'The value is too short.',
  typeMismatch: 'The value does not match required format.',
  valueMissing: 'This field is required.',
  valid: '<empty>',
}

const isValid = ref(true)
const validityState = ref<keyof ValidityState>('valid')

const modelValue = defineModel()

function onBlurHandler(event: FocusEvent) {
  const input = event.target as HTMLInputElement
  if (input.validity.valid) {
    isValid.value = true
  }
  else {
    isValid.value = false
    for (const key in input.validity) {
      if (key !== 'valid' && input.validity[key as keyof ValidityState]) {
        validityState.value = key as keyof ValidityState
        break
      }
    }
  }
}
</script>

<template>
  <input
    v-model="modelValue"
    v-bind="$attrs"
    p="x-4 y-2"
    h-12
    w-96
    bg="transparent"
    outline="none active:none"
    class="gray-200 dark:gray-700"
    :class="{ 'border-pink-500': !isValid, 'text-pink-600': !isValid }"
    border="~ rounded"
    @blur="onBlurHandler"
  >
  <div v-show="!isValid" mt-1 text-pink-600>
    {{ props.messages?.[validityState] || VALIDATION_MESSAGES[validityState] }}
  </div>
</template>
