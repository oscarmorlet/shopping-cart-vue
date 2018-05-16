<template>
  <div>
    <h1>Carrito de compras</h1>
    <ul>
      <li v-for="product in products">
          {{product.title}} - {{product.price | currency}} - {{product.quantity}}
      </li>
    </ul>
    <p>Total: {{ total | currency }}</p>
    <button v-if="$store.state.cart.length > 0" @click="$store.dispatch('checkout')"> Checkout </button>
    <p v-if="$store.state.checkoutStatus">{{ $store.state.checkoutStatus }}</p>
  </div>
</template>

<script>
export default {
  computed: {
    products () {
      return this.$store.getters.cartProducts
    },
    total () {
      return this.$store.getters.cartTotal
    }
  }
}
</script>

<style>
</style>
