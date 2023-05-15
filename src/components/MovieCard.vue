<script>
import { toHandlers } from 'vue';

export default {
  data() {
    return {
      moviename: this.movie.original_title, // title of the movie
      moviealt: this.movie.original_title + " poster", // alt tag for the picture
      moviepath: 'https://image.tmdb.org/t/p/w185/' + this.movie.poster_path, // movie picture
    }
  },
  methods: {
    incrementAdultTickets()
    // send an event up the chain with the movie name and an incremented ticket value
    {
      this.$emit('updateAdult', this.moviename, this.adultTickets + 1);
    },
    incrementChildTickets()
    // send an event up the chain with the movie name and an incremented ticket value
    {
      this.$emit('updateChild', this.moviename, this.childTickets + 1);
    },
  },
  props: {
    movie: {
      // take a movie as a prop
      type: Object,
      default: {

       }
    },
    adultCount: {
      // take the adult count-tracking object as a prop
        type: Object,
        default: {

        }
    },
    childCount: {
      // take the chil count-tracking object as a prop
        type: Object,
        default: {

        }
    }
  },
  computed: 
  // these values derive from the props. Because the props depend on a value that is acquired asyncronously, they have null checks and default values for when the prop hasn't fully loaded
  {
    adultTickets() {
      if (this.adultCount != undefined) {
        return this.adultCount[this.moviename] // return the count for this movie
      }
      else
      {
        return 0
      }
    },
  childTickets() {
      if (this.childCount != undefined) {
        return this.childCount[this.moviename] // return the count for this movie
      }
      else
      {
        return 0
      }
    }
  }
}
</script>

<template>
  <div class="card" style="width: 18rem;">
    <img :src="moviepath" class="card-img-top" v-bind:alt="moviealt">
    <div class="card-body">
      <h5 class="card-title">{{ movie.original_title }}</h5>
      <p class="card-text">{{ movie.overview }}</p>
      <div class="d-flex justify-content-between">
        <!-- On click, increment adult tickets -->
        <a @click="incrementAdultTickets" class="btn btn-primary">Adult Ticket<span
            class="badge badge-pill badge-danger">{{ adultTickets }}</span></a>
        <!-- On click, increment adult tickets -->
        <a @click="incrementChildTickets" class="btn btn-primary">Child Ticket<span
            class="badge badge-pill badge-danger">{{ childTickets }}</span></a>
      </div>
    </div>
  </div>
</template>

<style scoped>
* {
  color: var(--color-text-light);
}

.card {
  margin: 1rem;
  background-color: darkolivegreen;
}

.btn {
  color: aliceblue;
}

.badge {
  background-color: red;
  border-radius: 50px;
  position: absolute;
  right: -10px;
  top: -10px;

  color: aliceblue;
}
</style>