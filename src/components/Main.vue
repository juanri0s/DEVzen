<template>
  <div>
    <h1 v-if="loading"> loading... </h1>
    <h1 v-if="error"> {{ error }} </h1>
    <article-card
      v-for="post in posts" :key="post.id"
      :url=post.url
      :title=post.title
      :author=post.user.name
      :description=post.description
    />
    <fish-button type="primary" v-on:click="getPosts">load more</fish-button>
  </div>
</template>

<script>
import axios from 'axios';
import ArticleCard from './ArticleCard';

export default {
  name: 'Main',
  components: {
    ArticleCard,
  },
  data() {
    return {
      pageNum: 0,
      posts: [],
      error: '',
      loading: false,
    };
  },
  methods: {
    async getPosts() {
      this.loading = true;
      this.incrementPage();
      await axios.get(`https://dev.to/api/articles?page=${this.pageNum}`)
        .then((response) => {
          this.loading = false;

          if (this.posts) {
            this.posts.push(...response.data);
          } else {
            this.posts = response.data;
          }

          // eslint-disable-next-line no-console
          console.log(this.posts);
        })
        .catch((e) => {
          this.pageNum = this.pageNum !== 0 ? this.decrementPage() : 0;
          this.loading = false;
          this.error = e;
        });
    },
    incrementPage() {
      this.pageNum = this.pageNum + 1;
    },
    decrementPage() {
      this.pageNum = this.pageNum - 1;
    },
  },
  mounted() {
    return this.getPosts();
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
</style>
