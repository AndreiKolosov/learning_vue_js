<template>
  <div class="dialog" v-if="show === true" @click="closeDialog">
    <div @click.stop class="dialog__container">
      <slot></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Dialog',
  props: {
    show: {
      type: Boolean,
      default: false,
    },
  },
  methods: {
    closeDialog() {
      this.$emit('update:show', false);
    },
  },
};
</script>

<style scoped>
.dialog {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  align-items: center;
  justify-content: center;
}
.dialog__container {
  padding: 10px;
  border-radius: 20px;
  background-color: #fff;
  min-height: 200px;
  min-width: 200px;
}
</style>
