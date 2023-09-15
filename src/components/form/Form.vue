<script setup lang="ts">
const props = defineProps<{
  submit?: Function
}>()

function submitHandler(event: Event) {
  const form = (event.target as HTMLFormElement)
  Object.values(form.elements).forEach((formElement) => {
    const element = formElement as HTMLFormElement

    if (element.type !== 'submit') {
      element.focus()
      element.blur()
    }
  })

  if (form.checkValidity() && props.submit)
    props.submit(event)
}
</script>

<template>
  <form novalidate @submit.prevent="submitHandler">
    <slot />
  </form>
</template>
