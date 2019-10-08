<template>
  <div class="big-product-container">
    <div class="product">
      <div class="product-img">
        <img class="sock" :src="image" />
        <!-- Binds src attribute to image from image()-->
      </div>
      <div class="product-info">
        <h1>{{ title }}</h1>
        <!-- title() -->
        <p v-if="inStock">In Stock</p>
        <p v-else :class="{ outOfStock: !inStock }">Out of Stock</p>
        <!-- Class binding based off of inStock() -->
        <p>Shipping: {{ shipping }}</p>
        <!-- shipping() -->

        <ul>
          <li class="socks-details-list" v-for="detail in details" :key="detail.id">{{ detail }}</li>
          <!-- list generation with key binding -->
        </ul>

        <div
          v-for="(variant, index) in variants"
          :key="variant.variantID"
          class="color-box"
          :style="{ backgroundColor: variant.variantColor }"
          @mouseover="updateProduct(index)"
        ></div>
        <!-- Updates product image and info based off of index from updateProduct(index) method -->
        <button
          v-on:click="addToCart"
          :disabled="!inStock"
          :class="{ disabledButton: !inStock }"
        >Add to Cart</button>
        <!-- button disabled when item is not in stock, and disabledButton class is only present when inStock is false -->
      </div>
    </div>

    <product-tabs :reviews="reviews" />
  </div>
</template>

<script>
import ProductTabs from "@/components/ProductTabs.vue";

export default {
  name: "product" /* name of product */,
  components: {
    ProductTabs
  },
  props: {
    /* Receive props from App.Vue, and specify prop name and Type */
    premium: Boolean
  },
  data() {
    return {
      product: "Socks",
      brand: "Vue Mastery",
      selectedVariant: 0,
      // image:
      //   "https://www.vuemastery.com/images/challenges/vmSocks-green-onWhite.jpg",
      // inStock: true,
      details: ["80% cotton", "20% polyester", "Gender-neutral"],
      variants: [
        {
          variantID: 2234,
          variantColor: "green",
          variantImage:
            "https://www.vuemastery.com/images/challenges/vmSocks-green-onWhite.jpg",
          variantQuantity: 10
        },
        {
          variantID: 2235,
          variantColor: "blue",
          variantImage:
            "https://www.vuemastery.com/images/challenges/vmSocks-blue-onWhite.jpg",
          variantQuantity: 0
        }
      ],
      reviews: []
    };
  },
  methods: {
    /* methods alter data permanently per session */
    addToCart() {
      this.$emit(
        "add-to-cart",
        this.variants[this.selectedVariant].variantID
      ); /* variant ID is being passed into add-to-cart, which is bound to the updateCart method in App.vue */
    },
    updateProduct(index) {
      this.selectedVariant = index;
    }
  },
  computed: {
    /* computed properties used for manipulating data together */
    title() {
      return this.brand + " " + this.product;
    },
    image() {
      return this.variants[this.selectedVariant].variantImage;
    },
    inStock() {
      return this.variants[this.selectedVariant].variantQuantity;
    },
    shipping() {
      if (this.premium) {
        // premium is prop passed from App.vue
        return "Free";
      }
      return `$2.99`;
    }
  },
  mounted() {
    // A new Vue instance must be created for the reviews to be added into productReview!!! Currently this is not working
    eventBus.$on("review-submitted", productReview => {
      this.reviews.push(productReview);
    });
  }
};
</script>

<style scoped>
.big-product-container {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.product {
  display: flex;
  flex-direction: row;
}
.product-img {
  width: 50%;
}
.product-info {
  margin-top: 10px;
}
.sock {
  border: 1px solid #d8d8d8;
  width: 70%;
  margin: 40px;
  box-shadow: 0px 0.5px 1px;
}
.color-box {
  width: 40px;
  height: 40px;
  margin-top: 5px;
}
.disabledButton {
  background-color: #d8d8d8;
}
.outOfStock {
  text-decoration: line-through;
}
.socks-details-list {
  font-weight: bolder;
}
</style>