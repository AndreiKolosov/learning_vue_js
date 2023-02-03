<template>
  <section class="posts-section">
    <div class="controls">
      <Button class="controls__open-form" @click="openForm">Создать пост</Button>
      <Select v-model="selectedSort" :options="sortOptions" />
    </div>
    <Dialog v-model:show="isFormVisible">
      <PostForm @create="addPost" />
    </Dialog>
    <PostList :posts="sortedPosts" @remove="removePost" v-if="!isPostLoading" />
    <p v-else-if="isPostLoading">Loading ///</p>
  </section>
</template>

<script>
import PostForm from './components/PostForm.vue';
import PostList from './components/PostList.vue';
import axios from 'axios';

export default {
  components: {
    PostForm,
    PostList,
  },
  data() {
    return {
      posts: [],
      isFormVisible: false,
      isPostLoading: true,
      selectedSort: '',
      sortOptions: [
        { value: 'title', name: 'По названию' },
        { value: 'body', name: 'По содержанию' },
      ],
    };
  },
  methods: {
    addPost(post) {
      this.posts.push(post);
      this.isFormVisible = false;
    },
    removePost(post) {
      this.posts = this.posts.filter((item) => item.id !== post.id);
    },
    openForm() {
      this.isFormVisible = true;
    },
    async getPosts() {
      try {
        const { data: posts } = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=10');
        this.posts = posts;
        this.isPostLoading = false;
      } catch (error) {
        alert(error.message);
      }
    },
  },
  mounted() {
    this.getPosts();
  },
  computed: {
    sortedPosts() {
      return [...this.posts].sort((post1, post2) => {
        return post1[this.selectedSort]?.localeCompare(post2[this.selectedSort]);
      });
    },
  },
  watch: {
    // одноименная с моделью
    // selectedSort(newValue) {
    //   this.posts.sort((post1, post2) => {
    //     return post1[newValue]?.localeCompare(post2[newValue]);
    //   });
    // },
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

.controls {
  display: flex;
  justify-content: space-around;
}

.controls__open-form {
  max-width: 300px;
}
</style>
