<template>
  <div id="app">
    <div class="cart">
      <p>Cart: {{ cart.length }}</p>
    </div>
    <product :premium="premium" @add-to-cart="updateCart" />
    <!-- Listening for DOM event addToCart method in Product.vue, which is $emitting to add-to-cart and passing the item's ID here in the parent -->
    <!-- premium attribute being binded to component -->
  </div>
</template>

<script>
import Product from "@/components/Product.vue";

export default {
  name: "app",
  components: {
    Product
  },
  data() {
    return {
      premium: false /* prop being passed to Product component */,
      cart: []
    };
  },
  methods: {
    updateCart(id) {
      /* receiving id from addToCart method in child and pushing that id into cart array in data */
      this.cart.push(id);
    }
  }
};
</script>

<style>
body {
  font-family: tahoma;
  color: #282828;
  margin-bottom: 4em;
}
.cart {
  display: flex;
  justify-content: flex-end;
  padding-right: 5em;
}
</style>
