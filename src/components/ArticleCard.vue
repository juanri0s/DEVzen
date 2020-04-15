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
      :href=brandingUrl>
      <fish-image
        :url="require('../assets/dev_logo.png')"
        alt="Dev.to logo"
        style="max-height: 450px; max-width: 200px;"
      />
    </a>

    <a :href=url tabindex="0">
      <h2>{{ title }}</h2>
    </a>
    <p>{{ tags }}</p>
  </div>
</template>

<script>
import App from '../constants/app';

export default {
  name: 'ArticleCard',
  props: ['image', 'url', 'title', 'tags'],
  data() {
    return {
      brandingUrl: App.DEV_TO_BRANDING_URL,
      logoPath: App.DEV_TO_LOGO_PATH,
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
</style>
