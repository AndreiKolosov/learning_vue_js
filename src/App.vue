<template>
  <section class="posts-section">
    <Input v-model="searchQuery" placeholder="Search..." />
    <div class="controls">
      <Button class="controls__open-form" @click="openForm">Создать пост</Button>
      <Select v-model="selectedSort" :options="sortOptions" />
    </div>
    <Dialog v-model:show="isFormVisible">
      <PostForm @create="addPost" />
    </Dialog>
    <PostList :posts="sortedAndSearchedPosts" @remove="removePost" v-if="!isPostLoading" />
    <p v-else-if="isPostLoading">Loading ///</p>
    <div ref="observer" class="observer"></div>
    <!-- <ul class="pagination">
      <li
        class="pagination__page"
        v-for="pageNum in totalPages"
        :key="pageNum"
        :class="{ pagination__page_current: page === pageNum }"
        @click="changePage(pageNum)"
      >
        <span>{{ pageNum }}</span>
      </li>
    </ul> -->
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
      searchQuery: '',
      page: 1,
      limit: 7,
      totalPages: 0,
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
    // changePage(pageNum) {
    //   this.page = pageNum;
    // },
    async getPosts() {
      try {
        const response = await axios.get('https://jsonplaceholder.typicode.com/posts', {
          params: {
            _page: this.page,
            _limit: this.limit,
          },
        });

        this.totalPages = Math.ceil(response.headers['x-total-count'] / this.limit);
        this.posts = response.data;
        this.isPostLoading = false;
      } catch (error) {
        alert(error.message);
      }
    },
    async getMorePosts() {
      try {
        this.page += 1;
        const response = await axios.get('https://jsonplaceholder.typicode.com/posts', {
          params: {
            _page: this.page,
            _limit: this.limit,
          },
        });

        this.totalPages = Math.ceil(response.headers['x-total-count'] / this.limit);
        this.posts = [...this.posts, ...response.data];
      } catch (error) {
        alert(error.message);
      }
    },
  },
  mounted() {
    this.getPosts();

    const options = {
      rootMargin: '40px',
      threshold: 1.0,
    };

    const callback = (entries, observer) => {
      if (entries[0].isIntersecting && this.page < this.totalPages) {
        this.getMorePosts();
      }
    };

    const observer = new IntersectionObserver(callback, options);

    observer.observe(this.$refs.observer);
  },
  computed: {
    sortedPosts() {
      return [...this.posts].sort((post1, post2) => {
        return post1[this.selectedSort]?.localeCompare(post2[this.selectedSort]);
      });
    },
    sortedAndSearchedPosts() {
      return this.sortedPosts.filter((post) => post.title.toLowerCase().includes(this.searchQuery.toLowerCase()));
    },
  },
  watch: {
    // page() {
    //   this.getPosts();
    // },
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
  padding: 10px;
  display: flex;
  justify-content: space-around;
}

.controls__open-form {
  max-width: 300px;
}

/* .pagination {
  list-style: none;
  display: flex;
  width: 100%;
  justify-content: center;
  gap: 15px;
}

.pagination__page {
  cursor: pointer;
  width: 25px;
  height: 25px;
  border: 1px solid green;
  display: flex;
  align-items: center;
  justify-content: center;
}

.pagination__page_current {
  background-color: green;
  color: #fff;
} */

.observer {
  height: 30px;
}
</style>
