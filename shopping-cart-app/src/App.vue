<template>
  <div id="app">
    <product :premium="premium" />
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
      premium: false /* prop being passed to Product component */
    };
  }
};
</script>

<style>
body {
  font-family: tahoma;
  color: #282828;
  margin: 0px;
}
</style>
