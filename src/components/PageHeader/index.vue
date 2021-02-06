<template>
  <div class="page_header">
      <img src="../../assets/logo.svg" alt="Anime List">
      <h2>Organize sua lista de animes</h2>

      <button @click="openModal">Adicionar anime</button>
    </div>
</template>

<script>
  export default {
    emits: ['openModal'],
    methods: {
      openModal() {
        this.$emit('openModal', {
          mode: 'create',
          anime: {
            id: 0,
            name: '',
            status: 'Status',
            watched: 0,
            totalEps: 0
          }
        });
      }
    }
  }
</script>

<style scoped src="./styles.css"></style>