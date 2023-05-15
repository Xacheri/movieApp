<script setup>
import 'bootstrap/dist/css/bootstrap.css'
import axios from 'axios'
import Cart from './components/ShoppingCart.vue'
import HomeView from './views/HomeView.vue'


</script>

<script>
  export default {
    data() {
      return{
        showCart: false,
        adultCountObj: { },
        childCountObj: { },
      }
    },
    methods: {
      toggleCart()
      // function to flip the flag that hides the cart
      {
        if(this.showCart)
        {
          this.showCart = false;
        }
        else{
          this.showCart = true;
        }
      },
      updateCount(adult, child)
      {
        // updates the local count objects
        this.adultCountObj = adult;
        this.childCountObj = child;
      }
    }
  }
</script>
<template>
  <header>
    <nav>
        <a class="display-6" id="nameLink">Z-Movies</a>
        <!-- toggle cart on click -->
        <button @click="toggleCart" id="cartIcon" class="btn"><img src="./assets/cart.svg" width="35"> </button>
    </nav>
    <div class="d-flex justify-content-center"><h1>Now Playing</h1></div>
  </header>

  <div class="d-flex flex-column-reverse flex-lg-row">
    <!-- HomeView recieves the count objects and will trigger updateCount when it sends the event of the same name -->
    <HomeView :adultCountObj='adultCountObj' :childCountObj='childCountObj' @updateCount='updateCount' class="flex-grow-1"></HomeView>
    <!-- Cart only renders when showCart is true, recieves the count objects and will trigger updateCount when it sends the event of the same name -->
    <Cart @updateCount='updateCount' v-if="showCart" :adultCountObj="adultCountObj" :childCountObj="childCountObj"></Cart>
  </div>
  
  
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
