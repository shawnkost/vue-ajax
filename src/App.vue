<template>
  <v-app>
    <Header />

    <v-main class="grey darken-4">
      <Home />
    </v-main>
  </v-app>
</template>

<script>
import Header from './components/Header';
import Home from './views/Home';

export default {
  name: 'App',

  components: {
    Header,
    Home
  },

  data: () => ({
    //
  }),
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
