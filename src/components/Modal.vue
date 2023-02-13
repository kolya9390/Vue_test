<template>
  <div class="modal" v-if="show">
    <div class="modal-content">
      <slot></slot>
      <button @click="close">Close</button>
    </div>
  </div>
</template>

<script>
import LoginForm from "@/components/auth/LoginForm.vue";

export default {
  components: {LoginForm},
  props: {
    show: {
      type: Boolean,
      default: false
    }
  },
  methods: {
    close() {
      this.$emit('close');
    }
  }
};
</script>
