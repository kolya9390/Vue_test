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
        const response = await axios.post('http://localhost:8080/user/signin',
            {
          email: this.form.username,
          password: this.form.password
        });
        localStorage.setItem('token', response.data.access_token);
        this.$router.push('/');
      } catch (error) {
        this.errorMessage = error.response.data.message;
      }
    }
  }
}
</script>
<style>
.auth-form {
  width: 400px;
  margin: 0 auto;
  text-align: center;
}
.form-group {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-bottom: 20px;
}
label {
  font-weight: bold;
  margin-bottom: 10px;
}
input {
  padding: 10px;
  font-size: 16px;
  border-radius: 5px;
  border: 1px solid lightgray;
}
</style>