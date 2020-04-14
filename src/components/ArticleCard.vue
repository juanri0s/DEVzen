<template>
  <div>
    <h1>{{ message }}</h1>
  </div>
</template>

<script>
export default {
  name: 'ArticleCard',
  props: ['message'],
  data() {
    return { };
  },
  mounted() {
  },
  created() {
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
</style>
