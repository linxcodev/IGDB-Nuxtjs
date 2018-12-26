<template lang="html">
  <div class="game-container">
    <nuxt-link to="/">&lt;&lt;&lt; Back</nuxt-link>
    <br><br><br><br>
    <a :href="game.url">
      <h1>{{game.name}}</h1>
      <p><small>{{game.slug}}</small></p>
      <p>
        Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do
        eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim
        ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut
        aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit
        in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
        Excepteur sint occaecat cupidatat non proident, sunt in culpa qui
        officia deserunt mollit anim id est laborum.
      </p>
    </a>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  asyncData ({ params }) {
   const cors = 'https://cors-anywhere.herokuapp.com/'

   return axios.get(`${cors}https://api-v3.igdb.com/games/${params.id}?fields=*`)
   .then((res) => {
     return { game: res.data[0] }
   })
 },
 head() {
   return {
     title: this.game.name + ' | GameSite'
   }
 }
}
</script>

<style scoped>
  a {
    text-decoration: none;
    text-align:center;
    color: black
  }
  .game-container {
    padding: 0 10%;
    width: 80%;
    margin: 0 auto;
  }
  a.nuxt-link-active {
    color: blue
  }
  a.nuxt-link-active:hover {
    text-decoration: underline;
  }
</style>
