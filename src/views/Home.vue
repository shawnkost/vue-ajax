<template>
  <v-container>
    <TopAnime />
    <TopAiringAnime />
  </v-container>
</template>

<script>
import TopAnime from '../components/TopAnime';
import TopAiringAnime from '../components/TopAiringAnime';

export default {
  name: 'Home',

  components: {
    TopAnime,
    TopAiringAnime,
  },
};
</script>

<style></style>
