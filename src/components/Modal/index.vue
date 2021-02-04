<template>
  <div class="modal-container" :style="{ display }">
    <div class="modal">
      <h1 class="close-modal" @click="changeOpen">X</h1>
    </div>
  </div>
</template>

<script>
  export default {
    props: {
      open: Boolean,
      mode: String,
      anime: Object,
    },
    computed: {
      display() {
        return this.open ? 'flex' : 'none';
      }
    },
    methods: {
      changeOpen() {
        this.$emit('changeOpen');
      }
    }
  }
</script>

<style scoped src="./styles.css" />