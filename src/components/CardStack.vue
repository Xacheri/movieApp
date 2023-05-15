<script setup>
    import MovieCard from './MovieCard.vue';
import Card from './MovieCard.vue'
    import axios from 'axios';
</script>

<script>
  export default {
    data(){
        return {
            movies: [], // array to be filled with movies
            API_KEY: "1d7d5f1fbc662e59150df2a01915df43",
            movieLimit: 3, // limit to fill the movies up to

            // our counts are stored here, where the cards are grouped. They are filled in with this format:
            // {
            //  moviename: numOfTickets,
            //  moviename: numOfTickets,
            //  moviename: numOfTickets,
            // }
            adultCountObj: { },
            childCountObj: { },
        }
    },
    methods: {

      getMovies() {
        axios("https://api.themoviedb.org/3/movie/now_playing?api_key="+this.API_KEY+"&language=en-US&page=1").then(
          (response) => {
          this.movies = response.data.results.slice(0, this.movieLimit); // fill the array with the first {movielimit} movies

          // initialize countObj values
          this.movies.forEach(movie => {
          this.adultCountObj[movie.original_title] = 0;
          this.childCountObj[movie.original_title] = 0;

          // update those counts up the chain
          this.$emit("updateCount", this.adultCountObj, this.childCountObj);
        });
        })

      },
      updateAdult(title, count)
      {
        this.adultCountObj[title] = count; // set the title movie's count to the number recieved

        // update the counts up the chain
        this.$emit("updateCount", this.adultCountObj, this.childCountObj);
      },
      updateChild(title, count){
        this.childCountObj[title] = count; // set the title movie's count to the number recieved

        // update the counts up the chain
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
        <!-- When the card sends update events(like on ticket increment), run our update function. Make one card for every movie in the array. The component recieves the count objects and a movie-->
        <Card @updateAdult="updateAdult" @updateChild="updateChild" v-for="movie in movies" :movie="movie" :adultCount="this.adultCountObj" :childCount="this.childCountObj"></Card>
    </div>
</template>
