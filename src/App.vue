<template>
  <div>
    <div class="nav-bar"></div>
    <Product :premium="premium" />
  </div>
</template>

<script>
import Product from './components/Product'

export default {
  name: "App",
  data: () => {
    return {
      premium: false
    }
  },
  components: {
    Product
  }
}
</script>
