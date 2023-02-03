<template>
  <div class="post">
    <Button @click="$emit('remove', post)" type="button">Удалить</Button>
    <h3 class="post__title"><strong>Название: </strong>{{ post.title }}</h3>
    <p class="post__body">{{ post.body }}</p>
  </div>
</template>

<script>
export default {
  props: {
    post: {
      type: Object,
      required: true,
    },
  },
};
</script>

<style scoped>
.post {
  padding: 12px;
  border: 3px solid darkgreen;
  display: grid;
  grid-template-areas:
    'title btn'
    'body body';
  grid-template-columns: 1fr max-content;
  align-items: start;
  gap: 8px;
}
.post__title {
  grid-area: title;
  font-weight: 600;
  font-size: 21px;
}
.post__body {
  grid-area: body;
  font-weight: 400;
  font-size: 16px;
  padding: 0 15px;
}
</style>
