 <template>
  <div class="product">
    <div class="product-image">
      <img :src="image" />
    </div>
    <div class="product-info">
      <a :href="link">
        <h1>{{ title }}</h1>
      </a>
      <p v-if="inStock > 10">In Stock</p>
      <p v-else-if="inStock <= 10 && inStock > 0">Selling fast!</p>
      <p v-else :class="{ lineThrough: true }">Out of Stock</p>
      <p v-show="premium">Hello! You are premium!</p>
      <p>Shipping is {{ shipping }}</p>
      <span v-show="onSale">On sale!</span>
      <Details :details="details" />
      <p>Sizes:</p>
      <ul>
        <li v-for="(size, index) in sizes" :key="index">{{ size }}</li>
      </ul>
      <p>Colours:</p>
      <div
        v-for="(variant, index) in variants"
        :key="variant.variantId"
        class="color-box"
        :style="{ backgroundColor: variant.variantColor }"
        @mouseover="updateProduct(index)"
      ></div>
      <p>
        <button
          v-on:click="addToCart"
          :disabled="!inStock"
          :class="{ disabledButton: !inStock }"
        >Add to cart</button>
      </p>
      <p>
        <button v-on:click="removeFromCart">Remove from cart</button>
      </p>

    </div>
  </div>
</template>

<script>
import Details from './Details'

export default {
  props: {
    premium: {
      type: Boolean,
      required: true
    }
  },
  data: () => {
    return {
      product: "Socks",
      brand: "Unknown Branded",
      selectedVariant: 0,
      link: "http://teeturtle.com",
      details: ["Amazing happy octopus", "BPA free"],
      variants: [
        {
          variantId: 1234,
          variantColor: "powderblue",
          variantImage: require("../assets/blue.jpg"),
          variantQuantity: 100,
          variantOnSale: true,
        },
        {
          variantId: 1235,
          variantColor: "mediumturquoise",
          variantImage: require("../assets/bluer.jpg"),
          variantQuantity: 10,
          variantOnSale: false,
        },
      ],
      sizes: ["8", "9", "10"],
    }
  },
  methods: {
    addToCart() {
      this.$emit('update-cart', true, this.variants[this.selectedVariant].variantId)
    },
    removeFromCart() {
      this.$emit('update-cart', false, this.variants[this.selectedVariant].variantId)
    },
    updateProduct(index) {
      this.selectedVariant = index
    },
  },
  computed: {
    title() {
      return `${this.brand} ${this.product}`
    },
    image() {
      return this.variants[this.selectedVariant].variantImage
    },
    inStock() {
      return this.variants[this.selectedVariant].variantQuantity
    },
    onSale() {
      return this.variants[this.selectedVariant].variantOnSale
    },
    shipping() {
      return this.premium ? "free!" : "£2.99."
    }
  },
  components: {
    Details
  }
}
</script>
