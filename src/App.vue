<template>
  <section class="posts-section">
    <PostForm @create="addPost" />
    <PostList :posts="posts" />
  </section>
</template>

<script>
import PostForm from './components/PostForm.vue';
import PostList from './components/PostList.vue';

export default {
  components: {
    PostForm,
    PostList,
  },
  data() {
    return {
      posts: [
        {
          id: 1,
          title: 'JS',
          body: 'Далеко-далеко за словесными, горами в стране гласных и согласных живут рыбные тексты.',
        },
        {
          id: 2,
          title: 'JS3',
          body: 'Далеко-далеко за словесными, горами в стране гласных и согласных живут рыбные тексты.',
        },
        {
          id: 3,
          title: 'JS12',
          body: 'Далеко-далеко за словесными, горами в стране гласных и согласных живут рыбные тексты.',
        },
      ],
    };
  },
  methods: {
    addPost(post) {
      this.posts.push(post);
    },
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.posts-section {
  padding: 15px;
  background-color: rgb(245, 244, 244);
  width: 100%;
  height: 100%;
}
</style>
