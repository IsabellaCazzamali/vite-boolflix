<script>
import axios from 'axios';
import AppHeader from './components/AppHeader.vue';
export default {
  name: 'App',
  data(){
    return {
      movies: [], 
      image: 'https://api.themoviedb.org/3/configuration&',
      searchMovie: ''
    }
  },
  components: {
    AppHeader
  },
  mounted() {
    axios.get ('https://api.themoviedb.org/3/discover/movie', {
      headers: {
      'Authorization': 'Bearer eyJhbGciOiJIUzI1NiJ9.eyJhdWQiOiJkOTEyODZmYzgwYjQzMGVjMDBjMDkzMDQzYTc2ODlkOCIsInN1YiI6IjY2MDcyOTNkOGEwZTliMDE3YzRkYWFjMiIsInNjb3BlcyI6WyJhcGlfcmVhZCJdLCJ2ZXJzaW9uIjoxfQ.-9d58jzGjZ-xwHoqGheDr2mBup6cqJAyjQK3srHGmvk'
      }
    })
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
}
</script>

<template>

  <AppHeader></AppHeader>

<div class="search_bar">
  <input type="text" name="searchMovie" placeholder="Type the name of a movie to search" v-model="searchMovie">

  <button @click="$emit('searched', [searchMovie])">Search</button>
</div>


  <div>
    <div class="movie" v-for="movie in movies">
      <img :src="movie.image.poster_path" alt="movie poster">
      <h3>{{ movie.title }}</h3>
      <h4>{{ movie.original_title }}</h4>
      <h5>{{ movie.original_language }}</h5>
      <h5>{{ movie.vote_average }}</h5>
    </div>
  </div>

</template>

<style>

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