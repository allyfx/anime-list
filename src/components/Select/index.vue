<template>
  <div @click="changeOpen" class="select_container">
    <span className="selected_option">{{ selectedOption }}</span>

    <span className="arrow_icon">V</span>

    <div v-if="open" class="select_modal">
      <template
        :key="option.id"
        v-for="(option, index) in options"
      >
        <option
          :value="option.value"
          @click="handleSelect(option.value)"
          class="select_option"
        >{{ option.value }}</option>
        <div v-if="index !== options.length - 1" class="divider" />
      </template>
      
    </div>
  </div>
</template>

<script>
export default {
  props: {
    options: {
      type: Array,
      default() {
        return [];
      }
    },
    selectedOption: {
      type: String,
      required: true,
    }
  },
  emits: ['handleSelect'],
  data() {
    return {
      open: false,
    };
  },
  methods: {
    changeOpen() {
      this.open = !this.open;
      console.log(this.open);
    },
    handleSelect(selected) {
      this.$emit('handleSelect', selected);
    }
  }
}
</script>

<style src="./styles.css" scoped />