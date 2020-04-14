<template>
  <div>
    <h1 v-if="loading"> loading... </h1>
    <h1 v-if="error"> {{ error }} </h1>
    <article-card
      v-for="post in posts" :key="post.id"
      :title=post.title
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
      posts: [],
      error: '',
      loading: false,
    };
  },
  methods: {
    async getPosts() {
      this.loading = true;
      await axios.get('https://dev.to/api/articles')
        .then((response) => {
          this.loading = false;
          this.posts = response.data.sort((a, b) => a.id - b.id);
          console.log(this.posts);
        })
        .catch((e) => {
          this.loading = false;
          this.error = e;
        });
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
