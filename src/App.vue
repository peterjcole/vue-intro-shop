<template>
  <div>
    <div class="nav-bar"></div>
    <div class="product">
      <div class="product-image">
        <img :src="image" />
      </div>
      <div class="product-info">
        <a :href="link">
          <h1>{{ product }}</h1>
        </a>
        <p v-if="inventory > 10">In Stock</p>
        <p v-else-if="inventory <= 10 && inventory > 0">Selling fast!</p>
        <p v-else>Out of Stock</p>
        <span v-show="onSale">On sale!</span>
        <p>Details:</p>
        <ul>
          <li v-for="(detail, index) in details" :key="index">{{ detail }}</li>
        </ul>
        <p>Sizes:</p>
        <ul>
          <li v-for="(size, index) in sizes" :key="index">{{ size }}</li>
        </ul>
        <p>Colours:</p>
        <ul v-for="variant in variants" :key="variant.variantId">
          <li @mouseover="updateProduct(variant.variantImage)">{{ variant.variantColor }}</li>
        </ul>
        <p>
          <button v-on:click="addToCart">Add to cart</button>
        </p>
        <p>
          <button v-on:click="removeFromCart">Remove from cart</button>
        </p>
        <div class="cart">
          <p>Cart ({{ cart }})</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data: () => {
    return {
      product: "Socks",
      image: require("./assets/blue.jpg"),
      link: "http://teeturtle.com",
      inventory: 8,
      onSale: true,
      details: ["Amazing happy octopus", "BPA free"],
      variants: [
        {
          variantId: 1234,
          variantColor: "blue",
          variantImage: require("./assets/blue.jpg"),
        },
        {
          variantId: 1235,
          variantColor: "also blue",
          variantImage: require("./assets/bluer.jpg"),
        },
      ],
      sizes: ["8", "9", "10"],
      cart: 0,
    };
  },
  methods: {
    addToCart() {
      this.cart += 1;
    },
    removeFromCart() {
      this.cart -= 1;
    },
    updateProduct(variantImage) {
      this.image = variantImage;
    },
  },
};
</script>
