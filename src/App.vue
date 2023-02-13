<script xmlns="http://www.w3.org/1999/html">
import LoginForm from './components/auth/LoginForm.vue'
import RegistrationForm from './components/auth/Registration.vue'
import Header from "@/components/Header.vue";
import Home_test from "@/components/Home_test.vue";
import TodoItem from "@/components/Todo.vue";
import Back from "@/components/Back.vue";
import Layout from "@/components/Layout.vue";
import Events from "@/components/Events.vue";
import Modal from "@/components/Modal.vue";
import auth from "@/components/auth/Authenticate.vue"
import Authenticate from "@/components/auth/Authenticate.vue";


export default {
  components: {
    Authenticate,
    auth,
    Modal,
    Events,
    Back,
    TodoItem,
    Header,
    LoginForm,
    RegistrationForm
  }
}
</script>


<template>
  <div>
    <Header></Header>
  <router-view />
  </div>
<div>
  <Authenticate/>
</div>
<div>
  <Events/>
  </div>

  <footer>
    <Back></Back>
  </footer>
</template>

