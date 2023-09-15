## Running the project locally

To run the project locally run:

```bash
pnpm install --frozen-lockfile
pnpm run dev
```

## Basic components

### Button

Button component that supports a loading state:

```vue
<Button :disabled="isDisabled" :loading="isLoading" />
```

### Input

Low level input component that can be used to both directly and as a base for specialized components, like EmailInput, NumberInput, etc.

```vue
<Input
  type="email"
  placeholder="email@example.com"
  :messages="{ typeMismatch: 'Please enter a valid email address.' }"
/>
```

The component supports validation out-of-the-box. To display custom validation messages pass an object of messages, where key is one of HTML5 native input [validation states](https://developer.mozilla.org/en-US/docs/Web/API/ValidityState).

There are specialized components added for convenience

```vue
<EmailInput v-model="email" required />

<PasswordInput v-model="password" required />
```

### Form

A form component that has built in validation support (uses native HTML5 validaiton). Accepts a `submit` handler which is called on submit only when the form is valid.

```vue
<Form :submit="handleSubmit">
```

## Composite components

### SignInForm

High level component for displaying a sign in form. Accepts `handleSignIn` prop, which is a function that is being called with the email and password input by user, only if they meet the validation criteria. `error` prop can be used to show generic error messages (e.g. incorrect email/pass).

Example usage:

```vue
<script setup lang="ts">
const signInError = ref('')

async function signIn(email, password) {
  fetch('<sign_in_endpoint_here>', { method: 'post', body: JSON.stringify({ email, password }) })
    .then((res) => {
      if (res.ok)
        return res.json()

      signInError.value = 'Invalid email or password.'
    })
    .then(() => {
      // successfully logged in
    })
    .catch(() => {
      isLoading.value = false
      signInError.value = 'Something went wrong.'
    })
</script>

<template>
  <SignInForm :handle-sign-in="signIn" :error="signInError" />
</template>
```

