<template>
  <div class="home">
    <section class="hero is-medium is-dark mb-6">
      <div class="hero-body has-text-centered">
        <p class="title mb-6">Welcome to Momis</p>
        <p class="subtitle">The no. 1 place for all things fashion</p>
      </div>
    </section>

    <div class="columns is-multiline">
      <div class="column is-12">
        <h2 class="is-size-2 has-text-centered">New Items</h2>
      </div>
      <ProductBox v-for="product in newProducts" v-bind:key="product.id" v-bind:product="product" />
      
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import ProductBox from '@/components/ProductBox.vue';

export default {
  name: 'HomeView',
  data() {
    return {
      newProducts: [],
    };
  },
  components: { ProductBox },
  mounted() {
    this.getNewProducts();
    document.title = 'Home | Momis';
  },
  methods: {
    async getNewProducts() {
      this.$store.commit('setIsLoading', true);
      await axios
        .get('/api/v1/new-products/')
        .then((response) => {
          this.newProducts = response.data;
        })
        .catch((error) => {
          console.log(error);
        });

      this.$store.commit('setIsLoading', false);
    },
  },
};
</script>
