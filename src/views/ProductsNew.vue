<template>
  <div class="products-new">
    <form v-on:submit.prevent="createProduct()">
      <h1>New Product</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      Name:
      <input type="text" v-model="newProductParams.name" />
      Price:
      <input type="text" v-model="newProductParams.price" />
      Description:
      <input type="text" v-model="newProductParams.description" />
      Image URL:
      <input type="text" v-model="newProductParams.image_url" />
      Item Count:
      <input type="text" v-model="newProductParams.itemcount" />
      Supplier ID:
      <input type="text" v-model="newProductParams.supplier_id" />
      <input type="submit" value="Submit" />
    </form>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      newProductParams: {},
      errors: [],
    };
  },
  created: function () {},
  methods: {
    createProduct: function () {
      axios
        .post("/products", this.newProductParams)
        .then((response) => {
          console.log("products create", response);
          this.$router.push("/products");
        })
        .catch((error) => {
          console.log("products create error", error.response);
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>
