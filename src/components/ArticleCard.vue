<template>
  <div>
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
  props: ['url', 'title', 'author', 'description'],
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
