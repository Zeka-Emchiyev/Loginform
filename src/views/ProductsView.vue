<template>
  <v-container fill-height>
    <v-row>
      <v-col cols="12" sm="4" v-for="product in products">
        <v-card class="mx-auto" max-width="400">
          <h3>{{product.title}}</h3>
          <v-img class="white--text align-end" height="200px" :src="product.thumbnail">
          </v-img>
          <p> ${{product.price}}</p>
          <p>{{product.description}}</p>

        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import axios from 'axios'
export default {
  name: 'ProductsView',

  data() {
    return {
      products: ''
    };
  },

  mounted() {
    this.getProducts()
  },

  methods: {
    getProducts() {
      axios.get('https://dummyjson.com/products')
        .then(response => {
          this.products = response.data.products
          console.log(this.products)
        })

    }
  },
};
</script>

<style lang="scss" scoped>

</style>