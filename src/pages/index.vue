<script setup lang="ts">
defineOptions({
  name: 'IndexPage',
})

const signInError = ref('')
const router = useRouter()

function signIn() {
  // fetch('<sign_in_endpoint_here>', { method: 'post', body: JSON.stringify({ email, password }) })
  //   .then((res) => {
  //     if (res.ok)
  //       return res.json()

  //     error.value = 'Invalid email or password.'
  //   })
  //   .then(() => {
  //     router.push('/hi')
  //   })
  //   .catch(() => {
  //     isLoading.value = false
  //     error.value = 'Something went wrong.'
  //   })

  return new Promise<void>(resolve => setTimeout(() => {
    router.push('/hi')
    resolve()
  }, 2000))
}
</script>

<template>
  <SignInForm :handle-sign-in="signIn" :error="signInError" />
</template>
