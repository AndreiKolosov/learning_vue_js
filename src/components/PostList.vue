<template>
  <ul class="posts-list" v-if="posts.length > 0">
    <TransitionGroup name="post-list">
      <li v-for="post in posts" :key="post.id">
        <PostItem :post="post" @remove="$emit('remove', post)" />
      </li>
    </TransitionGroup>
  </ul>
  <p v-else class="posts__hint">Постов нет =(</p>
</template>

<script>
import { TransitionGroup } from 'vue';
import PostItem from './PostItem.vue';

export default {
  components: { PostItem, TransitionGroup },
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

/* animation */
.post-list-item {
  display: inline-block;
  margin-right: 10px;
}

.post-list-enter-active,
.post-list-leave-active {
  transition: all 0.5s ease;
}

.post-list-enter-from,
.post-list-leave-to {
  opacity: 0;
  transform: translateX(30px);
}
.post-list-move {
  transition: transform 0.8s ease;
}
</style>
