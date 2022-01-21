<template>
  <v-app>
    <Header />

    <v-main class="grey darken-4">
      <router-view @clicked="onClickChild" :malId="malId"></router-view>
    </v-main>
  </v-app>
</template>

<script>
import Header from './components/Header';

export default {
  name: 'App',

  components: {
    Header,
  },

  data() {
    return {
      malId: 0,
    };
  },

  methods: {
    onClickChild(value) {
      this.malId = value;
    },
  },
};
</script>
<style>
@font-face {
  font-family: 'League Spartan';
  font-weight: bold;
  src: url('./fonts/LeagueSpartan-Bold.otf') format('opentype');
}
@import url('https://fonts.googleapis.com/css2?family=Libre+Baskerville&display=swap');
</style>
