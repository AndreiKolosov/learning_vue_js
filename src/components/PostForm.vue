<template>
  <form class="form" @submit.prevent>
    <legend class="form__legend">Создание поста</legend>
    <input v-model="post.title" class="form__input" type="text" placeholder="Название" />
    <textarea
      v-model="post.body"
      class="form__textarea"
      name="postBody"
      id=""
      cols="30"
      rows="10"
      placeholder="Далеко-далеко за словесными, горами в стране гласных и согласных живут рыбные тексты..."
    ></textarea>
    <Button class="form__btn" @click="addPost">Добавить пост</Button>
  </form>
</template>

<script>
import Button from './UI/Button.vue';

export default {
  data() {
    return {
      post: {
        title: '',
        body: '',
      },
    };
  },
  methods: {
    addPost() {
      this.post.id = (Math.random() * 10).toString().replace('.', '');
      this.$emit('create', this.post);
      this.post = {
        title: '',
        body: '',
      };
    },
  },
  components: { Button },
};
</script>

<style scoped>
.form {
  width: 100%;
  border: 2px solid darkgreen;
  border-radius: 15px;
  padding: 10px;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 5px;
}
.form__legend {
  font-size: 24px;
  font-weight: 600;
}
.form__input {
  width: 100%;
  height: 30px;
  padding: 5px;
}
.form__textarea {
  width: 100%;
  padding: 5px;
}
.form__btn {
  max-width: 300px;
}
</style>
