<template>
  <div id="app">
    <h1> {{ header }} </h1>
    <router-view/>
  </div>
</template>

<script>
import App from './constants/app';

export default {
  name: 'App',
  data() {
    return {
      header: App.APP_NAME,
    };
  },
};
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 20px;
}
</style>
