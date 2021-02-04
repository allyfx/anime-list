<template>
  <div class="container">
    <Modal
      :open="openModal"
      :mode="modalMode"
      :anime="modalAnime"
      @changeOpen="changeOpen"
    />
    <PageHeader
      @openModal="setOpenModal"
    />
    <ListAnime
      @openModal="setOpenModal"
    />
  </div>
</template>

<script>
  import ListAnime from './components/ListAnime';
  import PageHeader from './components/PageHeader';
  import Modal from './components/Modal';

  export default {
    data() {
      return {
        openModal: false,
        modalMode: undefined,
        modaAnime: undefined,
      };
    },
    components: {
      ListAnime,
      PageHeader,
      Modal,
    },
    methods: {
      setOpenModal(mode) {
        this.openModal = true;
        this.modalMode = mode.mode;
        this.modalAanime = mode.anime;
      },
      changeOpen() {
        this.openModal = false;
      }
    }
  }
</script>

<style>
  html, body, #app {
    height: 100%;
    padding: 0;
    margin: 0;
    box-sizing: border-box;
  }
  .container {
    position: relative;
    height: 100%;
    background: url('./assets/BG.png') center;
    background-repeat: repeat-y;
    overflow: hidden;

    display: flex;
    flex-direction: column;
    align-items: center;

    font-family: 'Nunito', sans-serif;
  }
</style>
