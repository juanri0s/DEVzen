<template>
  <div>
    <h2>{{ title }} </h2>
  </div>
</template>

<script>
export default {
  name: 'ArticleCard',
  props: ['title'],
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
</style>
