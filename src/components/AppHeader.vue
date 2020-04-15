<template>
  <div class="header">
    <a href="/">
      <h1 class="header-titles">{{ appTitle }}</h1>
    </a>
  </div>
</template>

<script>
export default {
  name: 'AppHeader',
  props: ['appTitle'],
  data() {
    return {};
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.header {
  margin-bottom: 100px;
  background-color: #000;
  -webkit-box-shadow: 0 8px 6px -6px #999;
  -moz-box-shadow: 0 8px 6px -6px #999;
  box-shadow: 0 9px 6px -6px #999;
}

h1.header-titles {
  display: inline;
  font-family: Joystick;
  font-size: 5em;
  letter-spacing: 4px;
  color: #FFF;
}
</style>
