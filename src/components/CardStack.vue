<script setup>
    import MovieCard from './MovieCard.vue';
import Card from './MovieCard.vue'
    import axios from 'axios';
</script>

<script>
  export default {
    data(){
        return {
            movies: [],
            API_KEY: "1d7d5f1fbc662e59150df2a01915df43",
            movieLimit: 3,
            adultCountObj: { },
            childCountObj: { },
        }
    },
    methods: {

      getMovies() {
        axios("https://api.themoviedb.org/3/movie/now_playing?api_key="+this.API_KEY+"&language=en-US&page=1").then(
          (response) => {
          this.movies = response.data.results.slice(0, this.movieLimit);
          console.log(this.movies);
          this.movies.forEach(movie => {
          this.adultCountObj[movie.original_title] = 0;
          this.childCountObj[movie.original_title] = 0;
          this.$emit("updateCount", this.adultCountObj, this.childCountObj);
        });
        })

      },
      updateAdult(title, count)
      {
        this.adultCountObj[title] = count;
        console.log(this.adultCountObj);
        this.$emit("updateCount", this.adultCountObj, this.childCountObj);
      },
      updateChild(title, count){
        this.childCountObj[title] = count;
        console.log(this.childCountObj);
        this.$emit("updateCount", this.adultCountObj, this.childCountObj);
      }
    },
    beforeMount() {
      this.getMovies();
    }
  }
</script>

<template>
    <div class="d-flex justify-content-around flex-wrap">
        <Card @updateAdult="updateAdult" @updateChild="updateChild" v-for="movie in movies" :movie="movie" :adultCount="this.adultCountObj" :childCount="this.childCountObj"></Card>
    </div>
</template>
