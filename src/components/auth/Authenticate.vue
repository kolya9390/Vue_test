<template>
  <div class="auth-form">
    <h2 v-if="isLoggedIn">Hello, {{ username }}!</h2>
    <h2 v-else>Login</h2>
    <form v-if="!isLoggedIn" @submit.prevent="loginUser">
      <div class="form-group">
        <label for="email">Email:</label>
        <input
            type="email"
            id="email"
            name="email"
            v-model="form.email"
            required
        />
      </div>
      <div class="form-group">
        <label for="password">Password:</label>
        <input
            type="password"
            id="password"
            name="password"
            v-model="form.password"
            required
        />
      </div>
      <div class="form-group">
        <button type="submit" class="btn btn-primary">Login</button>
        <button v-if="showRegistration" type="button" class="btn btn-secondary" @click="showRegistration = false">Cancel</button>
      </div>
      <p v-if="errorMessage" class="error-message">{{ errorMessage }}</p>
    </form>
    <div v-else>
      <button class="btn btn-primary" @click="logoutUser">Logout</button>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      form: {
        email: "",
        password: "",
      },
      errorMessage: "",
      showRegistration: false,
    };
  },
  computed: {
    isLoggedIn() {
      return localStorage.getItem("token") !== null;
    },
    username() {
      return localStorage.getItem("username") || "User";
    },
  },
  methods: {
    async loginUser() {
      try {
        const response = await axios.post(
            "http://localhost:8080/user/signin",
            "grant_type=&username=" +
            this.form.email +
            "&password=" +
            this.form.password +
            "&scope=&client_id=&client_secret=",
            {
              headers: {
                "Content-Type": "application/x-www-form-urlencoded",
              },
            }
        );
        localStorage.setItem("token", response.data.access_token);
        localStorage.setItem("username", response.data.username);
        this.$emit("login-success");
      } catch (error) {
        console.error(error);
        this.errorMessage = "Invalid email or password";
      }
    },
    logoutUser() {
      localStorage.removeItem("token");
      localStorage.removeItem("username");
      this.$emit("logout-success");
    },
  },
};
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