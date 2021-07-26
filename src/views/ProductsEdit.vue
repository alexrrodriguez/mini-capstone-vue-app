<template>
  <div class="products-edit">
    <h1>Edit Product</h1>
    <form v-on:submit.prevent="updateProduct(product)">
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      Name:
      <input type="text" v-model="product.name" />
      Price:
      <input type="text" v-model="product.price" />
      Description:
      <input type="text" v-model="product.description" />
      Image URL:
      <input type="text" v-model="product.image_url" />
      Item Count:
      <input type="text" v-model="product.itemcount" />
      Supplier ID:
      <input type="text" v-model="product.supplier_id" />
      <input type="submit" value="Update" />
    </form>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      product: {},
      errors: [],
    };
  },
  created: function () {
    axios.get("/products/" + this.$route.params.id).then((response) => {
      console.log("products show", response);
      this.product = response.data;
    });
  },
  methods: {
    updateProduct: function (product) {
      var editProductParams = product;
      axios
        .patch("/products/" + product.id, editProductParams)
        .then((response) => {
          console.log("products update", response);
          this.$router.push("/products");
        })
        .catch((error) => {
          console.log("products update error", error.response);
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>
