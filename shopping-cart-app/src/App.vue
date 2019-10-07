<template>
  <div id="app">
    <product />
  </div>
</template>

<script>
import Product from "@/components/Product.vue";

export default {
  name: "app",
  components: {
    Product
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
