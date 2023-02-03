<template>
  <ul class="posts-list">
    <li v-for="post in posts" :key="post.id" v-if="posts.length > 0">
      <PostItem :post="post" @remove="$emit('remove', post)" />
    </li>
    <li v-else>
      <p class="posts__hint">Постов нет =(</p>
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
.posts__hint {
  color: green;
}
</style>
