<template>
  <div class="products-index">
    <h1>All Products</h1>
    <div class="card" style="width: 18rem" v-for="product in products" v-bind:key="product.id">
      <img v-bind:src="product.image_url" v-bind:alt="product.name" />
      <div class="card-body">
        <h5 class="card-title">{{ product.name }}</h5>
        <p class="card-text">
          {{ product.description }}
        </p>
        <p>Item Count: {{ product.itemcount }}</p>
        <router-link class="btn btn-primary" v-bind:to="`/products/${product.id}`">More Details</router-link>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      products: [],
    };
  },
  created: function () {
    this.indexProducts();
  },
  methods: {
    indexProducts: function () {
      axios.get("/products").then((response) => {
        console.log("products index", response);
        this.products = response.data;
      });
    },
  },
};
</script>
