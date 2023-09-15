<script setup lang="ts">
const props = defineProps<{
  handleSignIn: (email: string, password: string) => Promise<void>
  error?: string
}>()

defineOptions({
  name: 'IndexPage',
})

const email = ref('')
const password = ref('')
const isLoading = ref(false)

async function handleSubmit() {
  isLoading.value = true

  await props.handleSignIn(email.value, password.value)
  isLoading.value = false
}
</script>

<template>
  <div>
    <p text-lg>
      Sign in
    </p>
    <p text-md op-75>
      <em>Please enter your email and password</em>
    </p>

    <div py-4 />

    <div v-show="error" pb-4 text-red-600>
      {{ error }}
    </div>

    <Form :submit="handleSubmit">
      <div py-2>
        <EmailInput v-model="email" required />
      </div>

      <div py-2>
        <PasswordInput v-model="password" required />
      </div>

      <div py-2>
        <Button :disabled="!(email && password)" :is-loading="isLoading">
          Sign in
        </Button>
      </div>
    </Form>
  </div>
</template>
