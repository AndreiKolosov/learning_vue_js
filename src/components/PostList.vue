<template>
  <ul class="posts-list">
    <li v-for="post in posts">
      <PostItem :post="post" />
    </li>
  </ul>
</template>

<script>
import PostItem from './PostItem.vue';

export default {
  components: { PostItem },
  props: {
    posts: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style scoped>
.posts-list {
  list-style: none;
  padding: 15px;
  display: flex;
  flex-direction: column;
  gap: 20px;
}
</style>
