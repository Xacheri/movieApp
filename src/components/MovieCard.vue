<script>
import { toHandlers } from 'vue';

  export default {
    data(){
      return {
        moviename: this.movie.original_title,
        moviealt: this.movie.original_title + " poster",
        moviepath: 'https://image.tmdb.org/t/p/w185/' + this.movie.poster_path,
        adultCount: 0,
        childCount: 0
      }
    },
    props: ['movie'],
    methods: {
        incrementAdultTickets(){
          this.adultCount++;
          this.$emit('updateAdult', this.movie.original_title, this.adultCount);
        },
        incrementChildTickets(){
          this.childCount++;
          this.$emit('updateChild', this.movie.original_title, this.childCount);
        }
    },
  }
</script>

<template>
    <div class="card" style="width: 18rem;">
        <img :src="moviepath" class="card-img-top" v-bind:alt="moviealt">
        <div class="card-body">
          <h5 class="card-title">{{ movie.original_title }}</h5>
          <p class="card-text">{{ movie.overview}}</p>
          <div class="d-flex justify-content-between">
            <a @click="incrementAdultTickets" class="btn btn-primary">Adult Ticket<span class="badge badge-pill badge-danger">{{ adultCount }}</span></a>
            <a @click="incrementChildTickets" class="btn btn-primary">Child Ticket<span class="badge badge-pill badge-danger">{{ childCount }}</span></a>
          </div>
        </div>
      </div>
</template>

<style scoped>
* {
  color: var(--color-text-dark);
}

.card {
  margin: 1rem;
}
.btn {
  color:aliceblue;
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