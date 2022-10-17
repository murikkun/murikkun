<template>
  <button type="button" class="add-btn" @click="changeModal">
    <img src="../assets/images/fab.svg" alt="">
  </button>
</template>

<script>
export default {
  methods: {
    changeModal(){
      this.$emit('changeModal', true)
    }
  }
}
</script>