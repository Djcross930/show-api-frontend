<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Welcome to Vue.js!",
      shows: []
    };
  },
  created: function () {
    this.indexShows()
  },
  methods: {
    indexShows: function () {
      console.log("yo")
      axios.get("/shows").then(response => {
        console.log(response.data)
        this.shows = response.data
      })
    }
  },
};
</script>

<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <div v-for="show in shows">
      <p> {{ show.name }} </p>
      <p>{{ show.episodes }}</p>
    </div>
  </div>
</template>

<style>
</style>