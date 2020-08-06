<template>
  <div>
    <div class="nav-bar"></div>
    <div class="cart">
      <p>Cart ({{ cart.length }})</p>
    </div>
    <Product :premium="premium" @update-cart="updateCart" />
  </div>
</template>

<script>
import Product from './components/Product'

export default {
  name: "App",
  data: () => {
    return {
      premium: false,
      cart: [],
    }
  },
  components: {
    Product
  },
  methods: {
    updateCart(add, id) {
      if (add) {
        this.cart.push(id)
      } else {
        const firstIndex = this.cart.findIndex(cartItem => cartItem === id)
        firstIndex != -1 && this.cart.splice(firstIndex, 1)
      }
    }
  }
}
</script>
