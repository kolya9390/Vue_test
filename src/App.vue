<script xmlns="http://www.w3.org/1999/html">
import Header from "@/components/Header.vue";
import Back from "@/components/Back.vue";
import Events from "@/components/Events.vue";
import Modal from "@/components/Modal.vue";
import Create_Event from "@/components/Create_Event.vue";




export default {
  components: {
    Modal,
    Events,
    Back,
    Header,
    Create_Event

  }
}
</script>


<template>
  <div>
    <Header></Header>
  <router-view />
  </div>
<div>
<Create_Event></Create_Event>
</div>
<div>
  <Events/>
  </div>

  <footer>
    <Back></Back>
  </footer>
</template>

