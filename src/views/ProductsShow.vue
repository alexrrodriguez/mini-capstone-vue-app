<template>
  <div class="products-show">
    <h2>{{ product.name }}</h2>
    <img v-bind:src="product.image_url" v-bind:alt="product.name" />
    <p>Description: {{ product.description }}</p>
    <p>Item Count: {{ product.itemcount }}</p>
    <router-link v-bind:to="`/products/${product.id}/edit`">Edit Product</router-link>
    |
    <button v-on:click="destroyProduct(product)">Delete Product</button>
    |
    <router-link to="/products">Back to all Products</router-link>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      product: {},
    };
  },
  created: function () {
    axios.get("/products/" + this.$route.params.id).then((response) => {
      console.log("products show", response);
      this.product = response.data;
    });
  },
  methods: {
    destroyProduct: function (product) {
      axios.delete("/products/" + product.id).then((response) => {
        console.log("product destroy", response);
        this.$router.push("/products");
      });
    },
  },
};
</script>
