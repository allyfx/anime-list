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
            :value="selectedAnime.name"
            @input="selectedAnime = { key: 'name', value: $event.target.value }"
          />
        </div>
        <div class="form_row">
          <label>Status: </label>
          <Select
            :options="options"
            :selectedOption="selectedAnime.status"
            @handleSelect="handleSelect"
          />
        </div>
        <div class="form_row">
          <label>Total eps.: </label>
          <input
            type="number"
            class="input_field"
            placeholder="Digite o total de episódios"
            :value="selectedAnime.totalEps"
            @input="selectedAnime = { key: 'totalEps', value: $event.target.value }"
          />
        </div>
        <div class="form_row">
          <label>Assistidos: </label>
          <input
            type="number"
            class="input_field"
            placeholder="Digite o total de episódios assistidos"
            :value="selectedAnime.watched"
            @input="selectedAnime = { key: 'watched', value: $event.target.value }"
          />
        </div>
        <div class="form_row">
          <label>Url imagem: </label>
          <input
            type="text"
            class="input_field"
            placeholder="Ex.: https://www..."
            :initialValue="selectedAnime.url"
            @input="selectedAnime = { key: 'url', value: $event.target.value }"
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
  import Select from '../Select';

  export default {
    props: {
      open: Boolean,
      mode: {
        type: String,
        default: 'create'
      },
      anime: {
        type: Object,
        default() {
          return {
            id: 0,
            name: '',
            status: 'Status',
            watched: 0,
            totalEps: 0
          };
        }
      },
    },
    data() {
      return {
        newAnime: this.anime,
        options: [
          {
            id: 1,
            value: 'Não começou'
          },
          {
            id: 2,
            value: 'Assistindo'
          },
          {
            id: 3,
            value: 'Terminou'
          },
        ]
      };
    },
    emits: ['changeOpen', 'submitAnime'],
    computed: {
      display() {
        return this.open ? 'flex' : 'none';
      },
      buttonTitle() {
        return this.mode === 'edit' ? 'Editar' : 'Adicionar'
      },
      selectedAnime: {
        set(data) {
          this.newAnime = Object.assign(
            {},
            this.newAnime,
            { [data.key]: data.value }
          );
        },
        get() {
          return this.newAnime;
        }
      }
    },
    watch: {
      anime(newAnim) {
        this.newAnime = Object.assign({}, newAnim);
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
            anime: {
              id: this.selectedAnime.id,
              name: this.selectedAnime.name,
              url: this.selectedAnime.url,
              watched: this.selectedAnime.watched,
              totalEps: this.selectedAnime.totalEps,
              status: this.selectedAnime.status,
            },
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
      handleSelect(selected) {
        this.newAnime.status = selected;
      }
    },
    components: {
      Select,
    }
  }
</script>

<style scoped src="./styles.css" />