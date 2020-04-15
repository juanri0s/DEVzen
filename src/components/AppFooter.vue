<template>
  <div class="footer">
    <small>
      &copy; Copyright 2020,
      <a :href=personal>
        juanri0s
      </a>
    </small>
  </div>
</template>

<script>
import Strings from '../constants/strings';

export default {
  name: 'AppFooter',
  data() {
    return {
      personal: Strings.PERSONAL_URL,
    };
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.footer {
  color: #FFF;
  background-color: #000;
  height: 50px;
  margin: auto;
  line-height: 50px;
}
</style>
