<template>
  <button class="btn">
    <slot></slot>
  </button>
</template>

<script>
export default {
  name: 'Button',
};
</script>

<style>
.btn {
  cursor: pointer;
  width: 100%;
  background-color: transparent;
  padding: 15px;
  border-radius: 10px;
  border: 1px solid green;
}
</style>
