<template>
  <div style="max-height: 600px;">
    <a
      v-if=image
      :href=image>
      <fish-image
        :url=image
        alt="Dev.to post cover image"
      />
    </a>
    <a
      v-else
      :href=brandingUrl
    >
      <fish-image
        :url="require('../assets/dev_logo.png')"
        alt="Dev.to logo placeholder"
        style="max-height: 450px; max-width: 200px;"
      />
    </a>

    <div class="post-title">
      <a
        :href=url
      >
        <h2>{{ title }}</h2>
      </a>
    </div>
    <fish-tag
      tabindex="0"
      :href="'https://dev.to/t/' + tag"
      :index=index
      v-for="(tag, index) in tags"
      :key="index + tag"
    >
      {{ tag }}
    </fish-tag>
  </div>
</template>

<script>
import App from '@/constants/app';

export default {
  name: 'Post',
  props: {
    image: {
      type: String,
      required: false,
    },
    url: {
      type: String,
      required: true,
    },
    title: {
      type: String,
      required: true,
    },
    tags: {
      type: Array,
      required: false,
    },
  },
  data() {
    return {
      brandingUrl: App.DEV_TO_BRANDING_URL,
    };
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}

a:hover {
  text-decoration: underline;
}

.post-title {
  margin-top: 20px;
  margin-bottom: 20px;
}
</style>
