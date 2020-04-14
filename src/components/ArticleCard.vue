<template>
  <div>
    <img
      v-if=image
      :src=image
      alt="replace"
    >
    <img
      v-else
      src="../assets/dev_logo.png"
      alt="replace"
      width="300"
      height="300">
    <a :href=url tabindex="1">
      <h2>{{ title }} </h2>
    </a>
    <p>{{ description }}</p>
    author: {{ author }}
  </div>
</template>

<script>
export default {
  name: 'ArticleCard',
  props: ['image', 'url', 'title', 'author', 'description'],
  data() {
    return { };
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
