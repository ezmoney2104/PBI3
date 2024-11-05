<template>
  <div id="app">
    <RegistrationForm />
    <LoginForm />
  </div>
</template>

<script>
import RegistrationForm from './components/RegistrationForm.vue'
import LoginForm from './components/LoginForm.vue'

export default {
  components: {
    RegistrationForm,
    LoginForm
  }
}
</script>

<style>
/* Add your styles here */
</style>
