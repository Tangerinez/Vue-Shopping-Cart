<template>
  <div class="product">
    <div class="product-img">
      <img class="sock" :src="image" />
    </div>
    <div class="product-info">
      <h1>{{ title }}</h1>
      <p v-if="inStock">In Stock</p>
      <p v-else :class="{ outOfStock: !inStock }">Out of Stock</p>

      <ul>
        <li class="socks-details-list" v-for="detail in details" :key="detail.id">{{ detail }}</li>
      </ul>

      <div
        v-for="(variant, index) in variants"
        :key="variant.variantID"
        class="color-box"
        :style="{ backgroundColor: variant.variantColor }"
        @mouseover="updateProduct(index)"
      ></div>
      <button
        v-on:click="addToCart"
        :disabled="!inStock"
        :class="{ disabledButton: !inStock }"
      >Add to Cart</button>
      <div class="cart">
        <p>Cart: {{ cart }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "product",
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
      cart: 0
    };
  },
  methods: {
    addToCart() {
      this.cart += 1;
    },
    updateProduct(index) {
      this.selectedVariant = index;
    }
  },
  computed: {
    title() {
      return this.brand + " " + this.product;
    },
    image() {
      return this.variants[this.selectedVariant].variantImage;
    },
    inStock() {
      return this.variants[this.selectedVariant].variantQuantity;
    }
  }
};
</script>

<style scoped>
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