<template>
  <div id="app">
    <app-header :appTitle=appTitle />
    <router-view/>
    <app-footer/>
  </div>
</template>

<script>
import App from './constants/app';
import AppHeader from './components/AppHeader';
import AppFooter from './components/AppFooter';

export default {
  name: 'App',
  components: {
    AppHeader,
    AppFooter,
  },
  data() {
    return {
      appTitle: App.APP_NAME,
    };
  },
};
</script>

<style>
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background-color: #f9fcfb;
}

@font-face {
  font-family: Joystick;
  src: url('./assets/Joystick.otf');
  font-weight: normal;
}
</style>
