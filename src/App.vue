<template>
  <div class="container">
    <Modal
      :open="openModal"
      :mode="modalMode"
      :anime="modalAnime"
      @changeOpen="changeOpen"
      @submitAnime="submitAnime"
    />
    <PageHeader
      @openModal="setOpenModal"
    />
    <ListAnime
      :animes="animes"
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
        modalAnime: undefined,
        animes: []
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
        this.animes.map(anime => {
          if (anime.id === mode.anime) {
            this.modalAnime = anime;
          }
        });
      },
      changeOpen() {
        this.openModal = !this.openModal;

        if (!this.openModal) {
          this.modalAnime = undefined;
          this.modalMode = undefined;
        }
      },
      submitAnime(state) {
        if (state.mode === 'edit') {
          let animeIndex = -1;
          this.animes.map((anim, index) => {
            if (anim.id === state.anime.id) {
              animeIndex = index;
            }
          });

          if (animeIndex) {
            this.animes.splice(animeIndex, 1, state.anime);
          }
        } else if(state.mode === 'create') {
          this.animes.push(state.anime);
        } else if(state.mode === 'delete') {
          let animeIndex = -1;
          this.animes.map((anim, index) => {
            if (anim.id === state.anime.id) {
              animeIndex = index;
            }
          });

          this.animes.splice(animeIndex, 1);
        }
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
