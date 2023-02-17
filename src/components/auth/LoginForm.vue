<template>
  <div class="auth-form">
    <h2>Login</h2>
    <form @submit.prevent="loginUser">
      <div class="form-group">
        <label for="email">email:</label>
        <input
            type="text"
            id="username"
            v-model="form.email"
            required
        />
      </div>
      <div class="form-group">
        <label for="password">Password:</label>
        <input
            type="password"
            id="password"
            v-model="form.password"
            required
        />
      </div>
      <div class="form-group">
        <button type="submit" class="btn btn-primary">Login</button>
      </div>
      <p v-if="errorMessage" class="error-message">{{ errorMessage }}</p>
    </form>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      form: {
        email: '',
        password: ''
      },
      errorMessage: ''
    }
  },
  methods: {
    async loginUser() {
      try {
        const response = await axios.post('http://localhost:8080/user/signin', {
          email: this.form.email,
          password: this.form.password
        });
        localStorage.setItem('token', response.data.access_token);
      } catch (error) {
        console.error(error);
      }
    }
  }
}

</script>