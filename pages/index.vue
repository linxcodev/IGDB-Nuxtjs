<template>
  <div class="container">
    <div class="game-container">
      <nuxt-link :to="'/games/' + game.id"
        v-for="game in games" :key="game.id" class="block mb-10">
        <span v-if="game.cover">
          <img :src="game.cover.url.replace('t_thumb', 't_cover_big')" alt="cover">
        </span>
        <span v-else>
          <img src="~/assets/img/No_cover.png" alt="cover" width="270">
        </span>
        <h5>{{game.name}}</h5>
        <span v-if="game.genres">
          <p>{{game.genres[0].name}}</p>
        </span>
        <span v-else><p>No Genres</p></span>
      </nuxt-link>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  asyncData ({ params }) {
    const cors = 'https://cors-anywhere.herokuapp.com/'

    return axios.get(`${cors}https://api-v3.igdb.com/games/?fields=name,genres.name,cover.*,popularity&order=popularity:desc&expand=genres,cover`)
     .then((res) => {
       return { games: res.data }
    })
 },
 head() {
   return {
     title: 'GameSite'
   }
 }
}
</script>

<style>

</style>
