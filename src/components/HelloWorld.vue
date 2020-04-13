<template>
  <div>
    <h1 v-if="loading"> loading... </h1>
    <div v-if="errors">
      <h1> here </h1>
      <h1> {{ errors }} </h1>
      <h1 v-for="error in errors" :key="error"> {{ error }} </h1>
    </div>
    <fish-button type="primary" v-on:click="getPosts">load more</fish-button>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      posts: [],
      errors: [],
      loading: false,
    };
  },
  methods: {
    getPosts: () => {
      this.loading = true;
      axios.get('https://dev.to/api/articles')
        .then((response) => {
          // eslint-disable-next-line no-console
          console.log(response);
          this.loading = false;
          this.posts = response;
        })
        .catch((e) => {
          this.loading = false;
          this.errors = e;
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
