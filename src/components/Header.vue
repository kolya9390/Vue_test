<template>
  <header>
    <nav class="header-left">
      <ul>
        <li><a href="/home">Home</a></li>
        <li><a href="#">About</a></li>
        <li><a href="#">Contact</a></li>
      </ul>
    </nav>
    <div class="header-right">
      <button class="header-btn" @click="openLoginModal">Login</button>
      <button class="header-btn">Registration</button>
    </div>
    <modal v-if="showLoginModal" @close="showLoginModal = false">
      <!-- форма для аунтификации пользователя -->
    </modal>
  </header>
</template>
<script>
import Modal from './Modal.vue';

export default {
  components: {
    Modal
  },
  data() {
    return {
      showLoginModal: false
    };
  },
  methods: {
    openLoginModal() {
      this.showLoginModal = true;
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
