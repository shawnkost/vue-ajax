<template>
  <v-container>
    <h1>Top Anime</h1>
    <v-sheet dark class="sheet">
      <v-slide-group
        class="py-4 pr-4"
        show-arrows="desktop"
        mobile-breakpoint="960"
      >
        <v-slide-item v-for="show in shows" :key="show.mal_id">
          <v-card
            class="ma-2 anime-card"
            :width="
              $vuetify.breakpoint.xs
                ? '200px'
                : $vuetify.breakpoint.sm
                ? '20%'
                : '50%'
            "
            :height="$vuetify.breakpoint.xs ? '450px' : 'auto'"
            light
            v-on:click="route(show.mal_id)"
          >
            <v-img class="align-end" :src="show.image_url" aspect-ratio=".75">
            </v-img>

            <v-card-title primary-title class="d-block">
              <p class="card-title mb-0">{{ show.title }}</p>
            </v-card-title>
            <v-card-text class="card-text">
              <p>Start date: {{ show.start_date }}</p>
              <p v-if="show.end_date">End date: {{ show.end_date }}</p>
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
    route(id) {
      this.$emit('clicked', id);

      this.$router.push({
        name: 'Anime',
      });
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

.card-text p {
  margin-bottom: 1em;
}

@media screen and (max-width: 960px) {
  h1 {
    margin: 0px 0px 20px 0px;
  }
}

@media screen and (max-width: 600px) {
  .card-title {
    font-size: 1rem;
  }
  .card-text {
    font-size: 0.8rem;
  }
}
</style>
