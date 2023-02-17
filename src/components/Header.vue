<template>
  <header>
    <nav class="header-left">
      <ul>
        <li><a href="/">Home</a></li>
        <li><a href="#">About</a></li>
        <li><a href="#">Contact</a></li>
      </ul>
    </nav>
    <div class="header-right">
      <button v-if="!isLoggedIn" class="header-btn" @click="showLoginModal = true; showRegistration = false">Login</button>
      <button v-if="!isLoggedIn" class="header-btn" @click="showRegistration = true; showLoginModal = false">Registration</button>
      <button v-if="isLoggedIn" class="header-btn" @click="logoutUser">Logout</button>
    </div>
    <modal v-if="showLoginModal" @close="showLoginModal = false">
      <!-- форма для аунтификации пользователя -->
    </modal>
  </header>
  <Registration v-if="showRegistration" @close="showRegistration = false" />
</template>

<script>
import Modal from './auth/Authenticate.vue';
import Registration from './auth/Registration.vue';

export default {
  components: {
    Modal,
    Registration
  },
  data() {
    return {
      showLoginModal: false,
      showRegistration: false
    };
  },
  computed: {
    isLoggedIn() {
      return localStorage.getItem('token') !== null;
    }
  },
  methods: {
    logoutUser() {
      localStorage.removeItem('token');
    }
  }
};
</script>


<style>
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 20px;
  background-color: #2427a8;
  color: #fff;
}

.header-left {
  display: flex;
}

.header-left ul {
  display: flex;
  list-style: none;
  margin: 0;
  padding: 0;
}

.header-left ul li a {
  color: #ffffff;
  text-decoration: none;
  padding: 0 10px;
}

.header-right {
  display: flex;
}

.header-btn {
  background-color: #f6ecec;
  color: #0e1812;
  border: none;
  padding: 10px 20px;
  border-radius: 5px;
  text-transform: uppercase;
  font-weight: bold;
  cursor: pointer;
  margin-left: 10px;
}
</style>
