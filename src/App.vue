<script setup>
import { RouterLink, RouterView } from 'vue-router'
import 'bootstrap/dist/css/bootstrap.css'
import axios from 'axios'


</script>

<script>
  export default {
    data() {
      return{
        showCart: false
      }
    }
  }
</script>
<template>
  <header>
    <nav>
        <RouterLink class="h4" to="/" id="nameLink">Z-Movies</RouterLink>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/about">About</RouterLink>
        <button id="cartIcon" class="btn"><img src="./assets/cart.svg" width="35"> </button>
      </nav>
  </header>

  <RouterView />
  
</template>

<style scoped>
* {
  color: var(--color-text);
}

#nameLink {
  color: var(--text-gold) !important;
  text-decoration: none;
}

#cartIcon {
  margin-left: auto;
  background-color: var(--text-gold);
}

nav {
  display: flex;
  width: 100%;
  font-size: 12px;
}

nav a.router-link-exact-active {
  color: var(--text-color);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  color: var(--text-gold);
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;
  }
}
</style>
