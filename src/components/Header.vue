<template>
  <header>
    <nav class="navbar navbar-expand-lg navbar-light bg-light" role="navigation" aria-label="Main Navigation">
      <a class="navbar-brand" href="#">My App</a>
      <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarNav">
        <ul class="navbar-nav mr-auto">
          <li class="nav-item active">
            <a class="nav-link" href="#">Home</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="#">About</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="#">Contact</a>
          </li>
        </ul>
        <div class="header-right">
          <button v-if="!loggedIn" class="btn btn-primary ml-2" @click="showLoginModal = true; showRegistration = false">Login</button>
          <button v-if="!loggedIn" class="btn btn-secondary ml-2" @click="showRegistration = true; showLoginModal = false">Registration</button>
          <button v-if="loggedIn" class="btn btn-primary ml-2" @click="logoutUser">Logout</button>
        </div>
      </div>
    </nav>
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
  background-image: linear-gradient(to bottom, rgba(152, 90, 39, 0.3), rgba(152, 90, 39, 0.38));
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 20px;
  background-color: #ffffff;
  color: #110202;
}

.header-right {
  display: flex;
  align-items: center;
}

@media (max-width: 768px) {
  .header-left ul {
    display: none;
  }
}

.navbar-nav li {
  margin-right: 10px;
}

.navbar-nav li:last-child {
  margin-right: 0;
}

.navbar-brand {
  font-size: 24px;
  font-weight: bold;
  margin-right: 30px;
}

.btn {
  font-size: 16px;
  font-weight: bold;
}

.btn-primary {
  background-color: #1a1a1a;
  border-color: #1a1a1a;
}

.btn-primary:hover {
  background-color: #323232;
  border-color: #323232;
}

.btn-secondary {
  background-color: #ffffff;
  border-color: #808080;
  color: #808080;
}

.btn-secondary:hover {
  background-color: #f0f0f0;
  border-color: #808080;
  color: #808080;
}

@media (max-width: 768px) {
  .header-left ul {
    display: none;
  }
}

</style>
