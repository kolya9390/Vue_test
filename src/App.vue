<script xmlns="http://www.w3.org/1999/html">
import Header from "@/components/Header.vue";
import Back from "@/components/Back.vue";
import Events from "@/components/Events.vue";
import Modal from "@/components/Modal.vue";




export default {
  components: {
    Modal,
    Events,
    Back,
    Header,

  }
}
</script>


<template>
  <div>
    <Header></Header>
  <router-view />
  </div>
<div>

</div>
<div>
  <Events/>
  </div>

  <footer>
    <Back></Back>
  </footer>
</template>

