<template>
  <div>
    <h1 style="text-align: center;">Registration</h1>
    <form style="display: flex; flex-direction: column; align-items: center;">
      <label for="name" style="margin-top: 1rem;">Name:</label>
      <input id="name" v-model="name" type="text" style="width: 300px; padding: 0.5rem; margin-top: 0.5rem;" />
      <label for="username" style="margin-top: 1rem;">Username:</label>
      <input id="username" v-model="username" type="text" style="width: 300px; padding: 0.5rem; margin-top: 0.5rem;" />
      <label for="email" style="margin-top: 1rem;">Email:</label>
      <input id="email" v-model="email" type="email" style="width: 300px; padding: 0.5rem; margin-top: 0.5rem;" />

      <label for="password" style="margin-top: 1rem;">Password:</label>
      <input id="password" v-model="password" type="password" style="width: 300px; padding: 0.5rem; margin-top: 0.5rem;" />

      <label for="confirmPassword" style="margin-top: 1rem;">Confirm Password:</label>
      <input id="confirmPassword" v-model="confirmPassword" type="password" style="width: 300px; padding: 0.5rem; margin-top: 0.5rem;" />

      <label for="birthdate" style="margin-top: 1rem;">Birthdate:</label>
      <input id="birthdate" v-model="birthdate" type="date" style="width: 300px; padding: 0.5rem; margin-top: 0.5rem;" />

      <button @click.prevent="submitRegistrationForm" style="margin-top: 1rem; padding: 0.5rem 1rem; background-color: lightblue;">Submit</button>
    </form>
  </div>
</template>
<script>
export default {
  data() {
    return {
      name: '',
      username: '',
      email: '',
      password: '',
      confirmPassword: '',
      birthdate: ''
    }
  },
  methods: {
    submitRegistrationForm() {
      // send a request to the server with the registration data
      // and handle the response
    }
  }
}
</script>