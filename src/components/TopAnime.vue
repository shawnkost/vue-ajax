<template>
  <v-container>
    <h1>Top Anime</h1>
    <v-sheet dark class="sheet">
      <v-slide-group class="py-4 pr-4" center-active show-arrows>
        <v-slide-item v-for="show in shows" :key="show.id">
          <v-card class="ma-2 sk-card" width="300px" light>
            <v-img class="align-end" height="350px" :src="show.image_url">
            </v-img>

            <v-card-title primary-title>
              <p class="card-title mb-0">{{ show.title }}</p>
            </v-card-title>
            <v-card-text class="card-text">
              <p>Start date: {{ show.start_date }}</p>
              <p>End date: {{ show.end_date }}</p>
            </v-card-text>
          </v-card>
        </v-slide-item>
      </v-slide-group>
    </v-sheet>
  </v-container>
</template>

<script>
export default {
  name: 'TopAnime',

  data() {
    return {
      shows: [],
    };
  },

  methods: {
    async getData() {
      try {
        let response = await fetch(`https://api.jikan.moe/v3/top/anime`);
        let temp = await response.json();
        this.shows = temp.top;
        console.log(this.shows);
      } catch (error) {
        console.log(error);
      }
    },
  },

  created() {
    this.getData();
  },
};
</script>

<style scoped>
h1 {
  color: white;
  font-family: 'League Spartan', sans-serif;
  font-size: 48px;
  margin-bottom: 20px;
}

.sheet {
  background: transparent;
}

.card-title {
  font-family: 'League Spartan', sans-serif;
}

.card-text {
  font-size: 16px;
  font-family: 'Libre Baskerville', serif;
  /* height: 100px; */
}
</style>
