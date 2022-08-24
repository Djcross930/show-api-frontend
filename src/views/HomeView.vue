<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Welcome to Vue.js!",
      shows: [],
      currentShow: {},
      newShow: {}
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
    },
    createShow: function () {
      axios.post("/shows", this.newShow).then(response => {
        this.shows.push(response.data)
        this.newShow.name = ""
        this.newShow.episodes = ""
      })
    },
    updateShow: function () {
      axios.patch(`/shows/${this.currentShow.id}`, this.currentShow).then(response => {
        console.log(response.data)
      })
    },
    destroyShow: function (theShow) {
      axios.delete("/shows/" + theShow.id).then(response => {
        console.log(response.data)
        var index = this.shows.indexOf(theShow)
        this.shows.splice(index, 1)
      })
    }
  },
};
</script>

<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <p>Name:<input type="text" v-model="newShow.name"> </p>
    <p>Episodes:<input type="text" v-model="newShow.episodes"></p>
    <button v-on:click="createShow()">Create Show</button>
    <div v-for="show in shows">
      <p> {{ show.name }} </p>
      <p>{{ show.episodes }}</p>
      <button v-on:click="showShow(show)">More info</button>
    </div>

    <dialog id="show-details">
      <form method="dialog">
        <p> {{ currentShow.name }}</p>
        <p> {{ currentShow.episodes }}</p>
        <hr />
        <hr />
        <p>Name:<input type="text" v-model="currentShow.name"></p>
        <p>Episodes<input type="text" v-model="currentShow.episodes"></p>
        <button v-on:click="updateShow">Update Show</button>
        <button v-on:click="destroyShow(currentShow)">Delete Show</button>
        <button>Close</button>
      </form>
    </dialog>
  </div>
</template>

<style>
</style>