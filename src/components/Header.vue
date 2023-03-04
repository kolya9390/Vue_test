<template>
  <header>
    <nav class="header-left" role="navigation" aria-label="Main Navigation">
      <ul>
        <li>Home</li>
        <li>About</li>
        <li>Contact</li>
      </ul>
    </nav>
    <div class="header-right">
      <button v-if="!loggedIn" class="btn btn-primary" @click="showLoginModal = true; showRegistration = false">Login</button>
      <button v-if="!loggedIn" class="btn btn-secondary" @click="showRegistration = true; showLoginModal = false">Registration</button>
      <button v-if="loggedIn" class="btn btn-primary" @click="logoutUser">Logout</button>
    </div>
    <Authenticate v-if="showLoginModal" @close="showLoginModal = false" @login-success="loginSuccess" />
  </header>
  <Registration v-if="showRegistration" @close="showRegistration = false" @register-success="registerUser" />
  <div v-if="successMessage" class="alert alert-success" role="alert">
    {{ successMessage }}
  </div>
</template>
<script>
import Authenticate from './auth/Authenticate.vue';
import Registration from './auth/Registration.vue';
export default {
  components: {
    Authenticate,
    Registration
  },
  data() {
    return {
      showLoginModal: false,
      showRegistration: false,
      username: 'Admin',
      successMessage: '',
      loggedIn: false
    };
  },
  computed: {
    isLoggedIn() {
      return localStorage.getItem('token') !== null;
    }
  },
  created() {
    this.username = localStorage.getItem('Hi');
    this.loggedIn = this.isLoggedIn;
    if (this.isLoggedIn) {
      this.showLoginModal = false;
      this.showRegistration = false;
    }
  },
  methods: {
    loginSuccess() {
      this.showLoginModal = false;
      this.loggedIn = true;
      this.successMessage = 'You have successfully logged in!';
    },
    logoutUser() {
      localStorage.removeItem('token');
      localStorage.removeItem('username');
      this.username = 'Admin';
      this.loggedIn = false;
      this.successMessage = 'You have successfully logged out!';
      this.showLoginModal = false;
      this.showRegistration = false;
    },
    registerUser() {
      this.successMessage = 'You have successfully registered!';
      this.showLoginModal = false;
      this.showRegistration = false;
    },
    cancelLogout() {
      this.showLoginModal = false;
      this.showRegistration = false;
    }
  }
};
</script>



<style>
header {
  background-image: linear-gradient(to bottom, rgba(152, 90, 39, 0.8), rgba(152, 90, 39, 0.8));
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 20px;
  background-color: #ffffff;
  color: #110202;
}

.header-left {
  display: flex;
  align-items: center;
}

.header-left ul {
  display: flex;
  list-style: none;
  margin: 0;
  padding: 0;
}

.header-left ul li {
  margin-right: 10px;
}

.header-left ul li a {
  color: #110202;
  text-decoration: none;
  font-weight: bold;
}

.header-right {
  display: flex;
  align-items: center;
}


.btn {
  margin-left: 10px;
  background-color: #110202;
  color: #ffffff;
  padding: 5px 10px;
  border-radius: 5px;
  text-decoration: none;
}

@media (max-width: 768px) {
  .header-left ul {
    display: none;
  }


  .burger span {
    display: block;
    width: 25px;
    height: 3px;
    background-color: #110202;
    margin: 5px;
    border-radius: 3px;
  }
}

</style>