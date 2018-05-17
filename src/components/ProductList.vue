<template>
  <div>
      <h1>Lista de productos</h1>
      <img
      v-if="loading"
      src="https://i.imgur.com/JfPpwOA.gif"
      >
      <ul v-else>
         <li v-for="product in products">
            {{ product.title }} - {{ product.price | currency }} - {{ product.inventory }}
            <button
            :disabled="!productIsInStock(product)"
            @click="addProductToCart(product)"
            >Agregar al carrito</button>

         </li>
      </ul>
  </div>

</template>

<script>
import {mapState, mapGetters, mapActions} from 'vuex'

export default {
  data () {
    return {
      loading: false
    }
  },

  computed: {
    ...mapState({
        products: state => state.products.items
    }),
    /*products () {
      return this.$store.state.products
    },*/
    ...mapGetters('products', {
        productIsInStock: 'productIsInStock'
    }),
    /*productIsInStock () {
      return this.$store.getters.productIsInStock
    }*/
  },

  methods: {
    ...mapActions({
        fetchProducts: 'products/fetchProducts',
        addProductToCart: 'cart/addProductToCart'
    }),
      /*addProductToCart (product) {
          this.$store.dispatch('addProductToCart', product)
      }*/
  },

  created () {
    this.loading = true
    this.fetchProducts()
    .then(() => this.loading = false)
  }
}
</script>

<style>
</style>
