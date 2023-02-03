<template>
  <select :value="modelValue" @change="changeOption" :placeholder="placeholderValue">
    <option disabled value="">Выбери из списка...</option>
    <option v-for="option in options" :key="option.value" :value="option.value">{{ option.name }}</option>
  </select>
</template>

<script>
export default {
  name: 'Select',
  props: {
    placeholderValue: String,
    modelValue: String,
    options: {
      type: Array,
      default: () => [],
    },
  },
  methods: {
    changeOption(e) {
      this.$emit('update:modelValue', e.target.value);
    },
  },
};
</script>

<style scoped></style>
