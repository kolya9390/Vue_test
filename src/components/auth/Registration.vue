<template>
  <div v-if="!showSuccessMessage" class="registration-form">
    <h2>REG</h2>
    <form @submit.prevent="signupUser">
      <div class="form-group">
        <label for="email">Email</label>
        <input id="email" v-model="email" type="email" required />
      </div>
      <div class="form-group">
        <label for="password">Password</label>
        <input id="password" v-model="password" type="password" required />
      </div>
      <button type="submit">registration</button>
    </form>
    <div v-if="showErrorMessage" class="error-message">
      User with this email already exists
    </div>
  </div>
  <div v-if="showSuccessMessage" class="success-message">
    Успешная регистрация, теперь вы можете аунтифицироваться на сайте.
  </div>
</template>
<script>
import axios from "axios";
export default {
  data() {
    return {
      email: "",
      password: "",
      showSuccessMessage: false,
      showErrorMessage: false,
    };
  },
  methods: {
    async signupUser() {
      try {
        await axios.post(
            "http://localhost:8080/user/signup",
            {
              email: this.email,
              password: this.password,
            }
        );
        this.showSuccessMessage = true;
        setTimeout(() => {
          this.$router.push("/");
        }, 3000);
      } catch (error) {
        console.error(error);
        if (error.response.status === 409) {
          this.showErrorMessage = true;
        }
      }
    },
  },
};
</script>

<style>
.registration-form {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin: 50px;
}

form {
  display: flex;
  flex-direction: column;
  width: 300px;
  margin-top: 20px;
}

.form-group {
  display: flex;
  flex-direction: column;
  margin-bottom: 10px;
}

label {
  margin-bottom: 5px;
}

input {
  padding: 5px;
  font-size: 16px;
}

button {
  margin-top: 20px;
  padding: 10px;
  font-size: 16px;
  background-color: #4CAF50;
  color: white;
  border: none;
  cursor: pointer;
}

.success-message {
  margin-top: 20px;
  font-size: 18px;
  text-align: center;
}
</style>
