<script setup>
  import CardsView from '../components/CardStack.vue'
  import axios from 'axios';
  import cart from '../components/ShoppingCart.vue'
</script>

<script>
  export default {
  data() {
    return {

    }
  },
  methods: {
    updateCount(adult, child)
    {
      // when there is an update to the counts, send it up the chain
      this.$emit('updateCount', adult, child);
    }
  },
  props: {
    adultCountObj: {
      type: Object,
      default: {

      }
  },
    childCountObj: {
      type: Object,
      default: {

      }
    }
  }
}
</script>
<template>
  <div>
    <main>
    <!-- Update HomeView's count objects on update in the Cardsvie -->
      <CardsView @updateCount='updateCount'></CardsView>
    </main>
  </div>
</template>

