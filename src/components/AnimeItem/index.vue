<template>
  <div class="anime-item-container">
    <img v-if="anime.url === undefined" src="../../assets/no-image.svg" alt="Sem imagem">
    <img v-else :src="anime.url">

    <div class="informations">
      <h2>Nome: <span v-if="anime.name !== undefined">{{ anime.name }}</span></h2>
      <h3>Status: <span v-if="anime.status !== undefined">{{ anime.status }}</span></h3>
      <h3>
        Eps. assistidos: 
        <span
          v-if="anime.watched !== undefined && anime.totalEps !== undefined"
        >
          {{ anime.watched }}/{{ anime.totalEps }}
        </span>  
      </h3>
    </div>

    <button @click="openModal">Editar</button>
  </div>
</template>

<script>
  export default {
    props: {
      anime: Object,
    },
    methods: {
      openModal() {
        this.$emit('openModal', {
          mode: 'edit',
          anime: this.anime,
        });
      }
    }
  }
</script>

<style scoped src="./styles.css" />