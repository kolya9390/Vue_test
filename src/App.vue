<script xmlns="http://www.w3.org/1999/html">
import Header from "@/components/Header.vue";
import Back from "@/components/Back.vue";
import Modal from "@/components/Modal.vue";
import GetEvents from "@/components/Event2.0/GetEvents.vue";




export default {
  components: {
    GetEvents,
    Modal,
    Back,
    Header

  },

}
</script>


<template>
  <div>
    <Header></Header>
  </div>
<GetEvents/>
<div>

</div>
<div>

  </div>

  <footer>
    <Back></Back>
  </footer>
</template>

