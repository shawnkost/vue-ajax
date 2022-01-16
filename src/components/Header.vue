<template>
  <v-app-bar app color="indigo darken-4" dark height="80">
    <v-toolbar-title class="header-title">AniManiac</v-toolbar-title>
    <v-spacer></v-spacer>
    <div class="d-flex align-center justify-space-between">
      <v-btn icon>
        <v-icon large>mdi-account-plus</v-icon>
      </v-btn>
      <v-text-field
        label="Search"
        placeholder="Search"
        rounded
        single-line
        hide-details
        append-icon="mdi-magnify"
        class="test"
      ></v-text-field>
    </div>
  </v-app-bar>
</template>
<script>
export default {};
</script>
<style scoped>
.header-title {
  font-family: 'League Spartan', sans-serif;
}
</style>
