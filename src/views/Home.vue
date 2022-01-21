<template>
  <v-container>
    <TopAnime @clicked="onClickChild" />
    <TopAiringAnime />
  </v-container>
</template>

<script>
import TopAnime from '@/components/TopAnime';
import TopAiringAnime from '@/components/TopAiringAnime';

export default {
  name: 'Home',

  components: {
    TopAnime,
    TopAiringAnime,
  },

  methods: {
    onClickChild(id) {
      this.$emit('clicked', id);
    },
  },
};
</script>

<style></style>
