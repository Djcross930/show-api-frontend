<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Welcome to Vue.js!",
      shows: [],
      currentShow: {}
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
    },
    showShow: function (theShow) {
      console.log(theShow)
      this.currentShow = theShow
      document.querySelector('#show-details').showModal();
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
      <button v-on:click="showShow(show)">More info</button>
    </div>

    <dialog id="show-details">
      <form method="dialog">
        <p> {{ currentShow.name }}</p>
        <p> {{ currentShow.episodes }}</p>
        <button>Close</button>
      </form>
    </dialog>
  </div>
</template>

<style>
</style>