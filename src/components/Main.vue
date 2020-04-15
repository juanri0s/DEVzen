<template>
  <div class="content">
    <fish-loader :active="loading"/>
    <h1 v-if="error"> {{ error }} </h1>
    <fish-row gutter="5" v-for="(posts, index) in chunkedPosts" :key="index">
      <fish-col span="8" v-for="post in posts" :key="post.id">
        <article-card
          :image=post.cover_image
          :url=post.url
          :title=post.title
          :tags=post.tags
        />
      </fish-col>
    </fish-row>

    <fish-button
      type="basic"
      shape="circle"
      size="massive"
      :aria-labelledby=loadMoreMessage
      v-if="!loading"
      v-on:click="getPosts">
        {{ loadMoreMessage }}
    </fish-button>
  </div>
</template>

<script>
import axios from 'axios';
import App from '../constants/app';
import Strings from '../constants/strings';
import ArticleCard from './ArticleCard';

export default {
  name: 'Main',
  components: {
    ArticleCard,
  },
  data() {
    return {
      loadMoreMessage: Strings.LOAD_MORE,
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
      await axios.get(`${App.DEV_TO_API_BASE_URL}${App.DEV_TO_API_PAGE_PARAM}${this.pageNum}`)
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
    chunk(array, chunk) {
      const chunkedArray = [];
      // eslint-disable-next-line no-plusplus
      for (let i = 0; i < array.length; i++) {
        const last = chunkedArray[chunkedArray.length - 1];
        if (!last || last.length === chunk) {
          chunkedArray.push([array[i]]);
        } else {
          last.push(array[i]);
        }
      }
      return chunkedArray;
    },
  },
  mounted() {
    return this.getPosts();
  },
  computed: {
    chunkedPosts() {
      return this.chunk(this.posts, 3);
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}

.content {
  margin-left: 70px;
  margin-right: 70px;
  margin-bottom: 50px;
}
</style>
