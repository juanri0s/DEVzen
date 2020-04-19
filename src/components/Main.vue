<template>
  <div class="content">
    <fish-loader :active="loading"/>
    <h1 v-if="error"> {{ error }} </h1>
    <div class="wrapper">
      <post
          v-for="post in posts"
          :key="post.id"
          :image=post.cover_image
          :url=post.url
          :title=post.title
          :tags=post.tag_list
        />
    </div>

    <button
      v-if="!loading"
      v-on:click="getPosts"
      type="button"
      class="button round"
    >
      {{ loadMore }}
    </button>
  </div>
</template>

<script>
import thwack from 'thwack';
import App from '@/constants/app';
import Strings from '@/constants/strings';
import Post from '@/components/Post';

export default {
  name: 'Main',
  components: {
    Post,
  },
  data() {
    return {
      loadMore: Strings.LOAD_MORE,
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
      await thwack.get(`${App.DEV_TO_API_BASE_URL}${App.DEV_TO_API_PAGE_PARAM}${this.pageNum}`)
        .then((response) => {
          this.loading = false;

          if (this.posts) {
            this.posts.push(...response.data);
          } else {
            this.posts = response.data;
          }
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

.button.round {
  border: none;
  border-radius: 10em;
  -webkit-box-shadow: 0 0 0 1px rgba(34, 36, 38, 0.1) inset;
  box-shadow: 0 0 0 1px rgba(34, 36, 38, 0.1);
  display: inline-block;
  line-height: 1.2em;
  min-height: 1.2em;
  white-space: nowrap;
  text-align: center;
  cursor: pointer;
  font-size: 1.25rem;
  padding: 0.785em 1em;
  background: #FFF;
  text-decoration: none;
}

.button.round:hover {
  -webkit-box-shadow: 0 0 0 1px rgba(34, 36, 38, 0.3) inset;
  box-shadow: 0 0 0 1px rgba(34, 36, 38, 0.3)
}

.button.round:focus {
  -webkit-box-shadow: 0 0 0 1px rgba(34, 36, 38, 0.3) inset;
  box-shadow: 0 0 0 1px rgba(34, 36, 38, 0.3)
}

.content {
  margin: 50px 70px;
  max-width: 100%;
}

.wrapper {
  display: grid;
  max-width: 100%;
  grid-template-columns: repeat(3, 1fr);
  grid-gap: 2rem;
}

@media only screen and (max-width: 1200px) {
  .wrapper {
    grid-template-columns: repeat(2, 1fr);
  }

  .content {
    margin-left: 30px;
    margin-right: 30px;
  }
}

@media only screen and (max-width: 800px) {
  .wrapper {
    grid-template-columns: none;
  }

  .content {
    margin-top: 30px;
    margin-left: 30px;
    margin-right: 30px;
  }
}
</style>
