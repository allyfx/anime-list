<template>
  <div class="page_header">
      <img src="../../assets/logo.svg" alt="Anime List">
      <h2>Organize sua lista de animes</h2>

      <button @click="openModal">Adicionar anime</button>
    </div>
</template>

<script>
  export default {
    methods: {
      openModal() {
        this.$emit('openModal', {
          mode: 'create',
          anime: {}
        });
      }
    }
  }
</script>

<style scoped src="./styles.css"></style>