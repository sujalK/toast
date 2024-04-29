<template>
  <button @click="show" class="btn">Show</button>
  <toast
      type="success"
      message="The data saved successfully"
      :show="showToast"
      @hide="hide"
  />
</template>
<script>
import Toast from "./components/Toast/Toast.vue";

export default {
  components: {
    Toast
  },
  data () {
    return {
      showToast: false
    }
  },
  methods: {
    show() {
      this.showToast = true;
    },
    hide() {
      this.showToast = false;
    }
  }
}
</script>
<style>

</style>
