<script>
import { toHandlers } from 'vue';

export default {
  data() {
    return {
      moviename: this.movie.original_title,
      moviealt: this.movie.original_title + " poster",
      moviepath: 'https://image.tmdb.org/t/p/w185/' + this.movie.poster_path,
    }
  },
  methods: {
    incrementAdultTickets() {
      this.$emit('updateAdult', this.moviename, this.adultTickets + 1);
    },
    incrementChildTickets() {
      this.$emit('updateChild', this.moviename, this.childTickets + 1);
    },
  },
  props: {
    movie: {
      type: Object,
      default: {

       }
    },
    adultCount: {
        type: Object,
        default: {

        }
    },
    childCount: {
        type: Object,
        default: {

        }
    }
  },
  computed: {
    adultTickets() {
      if (this.adultCount != undefined) {
        return this.adultCount[this.moviename]
      }
      else
      {
        return 0
      }
    },
  childTickets() {
      if (this.childCount != undefined) {
        return this.childCount[this.moviename]
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
        <a @click="incrementAdultTickets" class="btn btn-primary">Adult Ticket<span
            class="badge badge-pill badge-danger">{{ adultTickets }}</span></a>
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
  background-color: teal;
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