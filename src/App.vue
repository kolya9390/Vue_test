<script xmlns="http://www.w3.org/1999/html">
import Header from "@/components/Header.vue";
import Back from "@/components/Back.vue";
import Modal from "@/components/Modal.vue";
import Eventlist from "@/components/Event2.0/Eventlist.vue";




export default {
  components: {
    Eventlist,
    Modal,
    Back,
    Header

  },

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
  <Eventlist/>
  </div>

  <footer>
    <Back></Back>
  </footer>
</template>

