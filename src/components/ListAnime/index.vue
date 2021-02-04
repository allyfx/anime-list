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
    data() {
      return {
        animes: [
          {
            id: 1,
            url: 'https://www.jbox.com.br/wp/wp-content/uploads/2020/09/detectiveconan-destacada.jpg',
            name: 'Detective Conan',
            status: 'Assistindo',
            watched: 592,
            totalEps: 995,
          },
          {
            id: 2,
            url: 'https://www.jbox.com.br/wp/wp-content/uploads/2020/09/detectiveconan-destacada.jpg',
            name: 'Detective Conan',
            status: 'Assistindo',
            watched: 592,
            totalEps: 995,
          },
          {
            id: 3,
            name: 'Detective Conan',
            status: 'Assistindo',
            watched: 592,
            totalEps: 995,
          },
          {
            id: 4,
            name: 'Detective Conan',
            status: 'Assistindo',
            watched: 592,
            totalEps: 995,
          },
          {
            id: 5,
            name: 'Detective Conan',
            status: 'Assistindo',
            watched: 592,
            totalEps: 995,
          },
          {
            id: 6,
            name: 'Detective Conan',
            status: 'Assistindo',
            watched: 592,
            totalEps: 995,
          },
        ]
      };
    },
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