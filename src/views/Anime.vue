<template>
  <h1>Test</h1>
</template>

<script>
export default {
  name: 'Anime',

  props: {
    malId: Number,
  },

  methods: {
    async getData() {
      console.log('anime', this.malId);
      try {
        let response = await fetch(
          `https://api.jikan.moe/v3/anime/${this.malId}`
        );
        let temp = await response.json();
        console.log('temp', temp);
        // this.shows = temp.top;
      } catch (error) {
        console.log(error);
      }
    },
  },

  mounted() {
    this.getData();
  },
};
</script>

<style></style>
