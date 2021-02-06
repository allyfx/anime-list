<template>
  <div class="list-container">
    <AnimeItem
      v-for="anime in animes"
      :key="anime.id"
      :anime="anime"
      @openModal="openModal"
    />
  </div>
</template>

<script>
  import AnimeItem from '../AnimeItem';

  export default {
    props: {
      animes: {
        type: Array,
        default() {
          return [];
        }
      }
    },
    emits: ['openModal'],
    components: {
      AnimeItem,
    },
    methods: {
      openModal(mode) {
        this.$emit('openModal', mode);
      }
    }
  }
</script>

<style scoped src="./styles.css" />