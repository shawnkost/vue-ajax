<template>
  <v-container>
    <h1>Top Anime</h1>

    <v-row>
      <v-col
        cols="12"
        sm="4"
        lg="2"
        v-for="show in shows"
        :key="show.id"
        pl-2
        pr-2
      >
        <v-card class="flex d-flex flex-column">
          <v-img :src="show.image_url"></v-img>
          <v-card-title primary-title>
            <h3 class="headline mb-0">{{ show.title }}</h3>
          </v-card-title>
          <v-card-text>
          <p>Start date: {{ show.start_date }}</p>
          <p>End date: {{ show.end_date }}</p>
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>
    <div>
      <ul v-for="show in shows" v-bind:key="show.id">
        <li>{{ show.title }}</li>
        <p>{{ show.body }}</p>
      </ul>
    </div>
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
</style>
