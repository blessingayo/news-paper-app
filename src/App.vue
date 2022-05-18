<template>
  <v-app>
    <div class="container" id="app">
      <SourceSelection v-on:sourceChanged="sourceChanged"></SourceSelection>

      <Newslist v-bind:source="source"></Newslist>
    </div>
  </v-app>
</template>

<script>
import SourceSelection from "./components/SourceSelection.vue"
import Newslist from "./components/Newslist.vue";
// import HomePage from "./components/HomePage"
export default {
  name: "App",

  components: {
    // HomePage
    SourceSelection,
    Newslist,
  },

  data: () => ({
    return: {
      source: "",
    },
  }),

  methods: {
    sourceChanged: function (source){
      this.source =source;
    }
  }
};
</script>

<style scoped>

/* #app {
  padding-top: 20px;
} */
</style>