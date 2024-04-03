<script>
import axios from 'axios';
import AppHeader from './components/AppHeader.vue';
export default {
  name: 'App',
  data(){
    return {
      api_key: "d91286fc80b430ec00c093043a7689d8",
      movies: [], 
      image: 'https://image.tmdb.org/t/p/w780/',
      searchMovie: ''
    }
  },
  components: {
    AppHeader
  },
  methods: {
    getMovies() {
      axios.get ('https://api.themoviedb.org/3/search/movie?api_key=' + this.api_key + '&query=' + this.searchMovie)
    .then(response => {
      console.log(response.data);
      console.log(response.data.results);
      console.log(this);
      this.movies = response.data.results;
    })
    .catch(error => {
      console.error(error);
    })
    }
  },
  mounted() {
    this.getMovies();
    /* axios.get ('https://api.themoviedb.org/3/search/movie?api_key=' + this.api_key + '&query=' + this.searchMovie 
    {
      headers: {
      'Authorization': 'Bearer eyJhbGciOiJIUzI1NiJ9.eyJhdWQiOiJkOTEyODZmYzgwYjQzMGVjMDBjMDkzMDQzYTc2ODlkOCIsInN1YiI6IjY2MDcyOTNkOGEwZTliMDE3YzRkYWFjMiIsInNjb3BlcyI6WyJhcGlfcmVhZCJdLCJ2ZXJzaW9uIjoxfQ.-9d58jzGjZ-xwHoqGheDr2mBup6cqJAyjQK3srHGmvk'
      }
    }
    )
    .then(response => {
      console.log(response.data);
      console.log(response.data.results);
      console.log(this);
      this.movies = response.data.results;
    })
    .catch(error => {
      console.error(error);
    }) */
  }
}
</script>

<template>

  <AppHeader></AppHeader>

<div class="search_bar">
  <input @keyup.enter="getMovies()" type="text" name="searchMovie" placeholder="Type the name of a movie to search" v-model="searchMovie">

  <button @click="getMovies()">Search</button>
</div>


  <div class="flex">
    <div class="movie" v-for="movie in movies">
      <img :src="image + movie.poster_path" alt="movie poster" width="200px">
      <h3>{{ movie.title }}</h3>
      <h4>{{ movie.original_title }}</h4>
      <h5>{{ movie.original_language }}</h5>
      <h5>{{ movie.vote_average }}</h5>
    </div>
  </div>

</template>

<style>

.flex{
  display: flex;
  flex-wrap: wrap;
}

.search_bar{
  margin-top: 1rem;
  margin-left: 1rem;
  &
  input, button {
    padding: 0.5rem;
    margin: 0.3rem;
    border-radius: 0.25rem;
    border-style: none;
  }
}

</style>