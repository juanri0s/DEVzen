<template>
  <div>
    <h1 v-if="loading"> loading... </h1>
    <h1 v-if="error"> {{ error }} </h1>
    <p v-if="posts"> {{ posts }} </p>
    <div>
      <p> here </p>
      <article-card :message=message />
    </div>
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
      message: 'hello everyone',
      posts: [],
      error: [],
      loading: false,
    };
  },
  methods: {
    getPosts: () => {
      this.loading = true;
      axios.get('https://dev.to/api/articles')
        .then((response) => {
          // eslint-disable-next-line no-console
          this.loading = false;
          this.posts = response.data;

          // this.posts.forEach((post) => {
          //   console.log('post', post);
          // });
        })
        .catch((e) => {
          this.loading = false;
          this.error = e;
        });
    },
  },
  created() {
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
