<script xmlns="http://www.w3.org/1999/html">
import Header from "@/components/Header.vue";
import Back from "@/components/Back.vue";
import Modal from "@/components/Modal.vue";
import GetEvents from "@/components/Event2.0/GetEvents.vue";
import FilteredEvents from "@/components/Event2.0/FilteredEvents.vue";




export default {
  components: {
    GetEvents,
    Modal,
    Back,
    Header,
    FilteredEvents

  },

}
</script>


<template>
  <div>
    <Header></Header>

  </div>

<GetEvents/>
<div>
<h1> Git?</h1>
</div>
<div>

  </div>

  <footer>
    <Back></Back>
  </footer>
</template>

