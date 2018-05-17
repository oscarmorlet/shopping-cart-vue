<template>
  <div>
    <h1>Carrito de compras</h1>
    <ul>
      <li v-for="product in products">
          {{product.title}} - {{product.price | currency}} - {{product.quantity}}
      </li>
    </ul>
    <p>Total: {{ total | currency }}</p>
    <button v-if="cartItems" @click="checkout"> Checkout </button>
    <p v-if="checkoutStatus">{{ checkoutStatus }}</p>
  </div>
</template>

<script>
import {mapState, mapGetters, mapActions} from 'vuex'

export default {
  computed: {
    ...mapGetters('cart', {
        products: 'cartProducts',
        total: 'cartTotal'
    }),

    /*products () {
      return this.$store.getters.cartProducts
    },
    total () {
      return this.$store.getters.cartTotal
    }*/
    ...mapState('cart', {
      checkoutStatus: state => state.checkoutStatus,
      cartItems: state => state.items.length > 0
    })
  },

  methods: {
    ...mapActions('cart', ['checkout'])
  }
}
</script>

<style>
</style>
