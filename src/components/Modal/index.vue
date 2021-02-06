<template>
  <div class="modal-container" :style="{ display }">
    <div class="modal">
      <h1 class="close-modal" @click="changeOpen">X</h1>
      <img v-if="newAnime.url" :src="newAnime.url">
      <img v-else src="../../assets/no-image.svg" alt="Sem imagem">

      <div class="form">
        <div class="form_row">
          <label>Nome: </label>
          <input
            type="text"
            class="input_field"
            placeholder="Digite o nome"
            v-model="newAnime.name"
          />
        </div>
        <div class="form_row">
          <label>Status: </label>
          <select name="" id=""></select>
        </div>
        <div class="form_row">
          <label>Total eps.: </label>
          <input
            type="number"
            class="input_field"
            placeholder="Digite o total de episódios"
            v-model="newAnime.totalEps"
          />
        </div>
        <div class="form_row">
          <label>Assistidos: </label>
          <input
            type="number"
            class="input_field"
            placeholder="Digite o total de episódios assistidos"
            v-model="newAnime.watched"
          />
        </div>
        <div class="form_row">
          <label>Url imagem: </label>
          <input
            type="text"
            class="input_field"
            placeholder="Ex.: https://www..."
            v-model="newAnime.url"
          />
        </div>
      </div>

      <div class="buttons">
        <button v-if="mode === 'edit'" class="remove_button" @click="deleteAnime">Remover</button>
        <button
          class="add_button"
          @click="submitAnime"
        >
          {{ buttonTitle }}
        </button>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        newAnime: {},
      };
    },
    props: {
      open: Boolean,
      mode: String,
      anime: {
        type: Object,
        default() {
          return {
            id: 0,
            name: '',
            status: '',
            watched: 0,
            totalEps: 0
          };
        }
      },
    },
    watch: {
      anime() {
        this.newAnime = this.anime;
      }
    },
    computed: {
      display() {
        return this.open ? 'flex' : 'none';
      },
      buttonTitle() {
        return this.mode === 'edit' ? 'Editar' : 'Adicionar'
      }
    },
    methods: {
      changeOpen() {
        this.$emit('changeOpen');
      },
      submitAnime() {
        if (this.mode === 'edit') {
          this.$emit('submitAnime', {
            mode: 'edit',
            anime: this.newAnime,
          });
        } else {
          this.$emit('submitAnime', {
            mode: 'create',
            anime: this.newAnime,
          });
        }
        this.changeOpen();
      },
      deleteAnime() {
        this.$emit('submitAnime', {
            mode: 'delete',
            anime: this.newAnime,
          });
        this.changeOpen();
      },
    }
  }
</script>

<style scoped src="./styles.css" />