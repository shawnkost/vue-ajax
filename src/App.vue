<template>
  <v-app>
    <Header />

    <v-main>
      <HelloWorld />
    </v-main>
  </v-app>
</template>

<script>
import HelloWorld from './components/HelloWorld';
import Header from './components/Header';
export default {
  name: 'App',

  components: {
    HelloWorld,
    Header,
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
