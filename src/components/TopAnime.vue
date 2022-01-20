<template>
  <v-container>
    <h1>Top Anime</h1>
    <v-sheet dark class="sheet">
      <v-slide-group
        class="py-4 pr-4"
        show-arrows="desktop"
        mobile-breakpoint="960"
      >
        <v-slide-item v-for="show in shows" :key="show.id">
          <v-card
            class="ma-2 anime-card"
            :width="
              $vuetify.breakpoint.xs
                ? '300px'
                : $vuetify.breakpoint.sm
                ? '20%'
                : '50%'
            "
            light
          >
            <v-img class="align-end" max-height="400px" :src="show.image_url">
            </v-img>

            <v-card-title primary-title class="d-block">
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
      let data = localStorage.getItem('topAnime');
      data = JSON.parse(data);

      if (!data?.shows || this.isDataOutdated(data)) {
        try {
          let response = await fetch(`https://api.jikan.moe/v3/top/anime`);
          let temp = await response.json();
          localStorage.setItem(
            'topAnime',
            JSON.stringify({ shows: temp.top, receivedAt: new Date() })
          );
          this.shows = temp.top;
        } catch (error) {
          console.log(error);
        }
      } else {
        this.shows = data.shows;
      }
    },
    isDataOutdated(receivedAt) {
      const checkDate = new Date(new Date().getTime() - 60 * 60 * 4 * 1000);
      return new Date(receivedAt).getTime() < checkDate.getTime();
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
  margin: 0px 0px 20px 50px;
}

.sheet {
  background: transparent;
}

.anime-card {
  text-align: center;
  border-radius: 10px !important;
}

.card-title {
  font-family: 'League Spartan', sans-serif;
}

.card-text {
  font-size: 16px;
  font-family: 'Libre Baskerville', serif;
}

@media screen and (max-width: 960px) {
  h1 {
    margin: 0px 0px 20px 0px;
  }
}
</style>
