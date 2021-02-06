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
      ListAnime,
      PageHeader,
      Modal,
    },
    methods: {
      setOpenModal(mode) {
        this.openModal = true;
        this.modalMode = mode.mode;
        this.modalAnime = mode.anime;
      },
      changeOpen() {
        this.openModal = false;
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
