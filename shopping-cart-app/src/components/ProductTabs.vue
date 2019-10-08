<template>
  <div>
    <span
      class="tab"
      :class="{ activeTab: selectedTab === tab}"
      v-for="(tab, index) in tabs"
      :key="index"
      @click="selectedTab = tab "
    >{{ tab }}</span>

    <div v-show="selectedTab === 'Reviews'">
      <p v-if="!reviews.length">There are no reviews yet.</p>
      <!-- Displays p-tag only if length is 0 -->
      <ul>
        <li v-for="review in reviews" :key="review.id">
          <p>{{ review.name }}</p>
          <p>Rating: {{ review.rating }}</p>
          <p>{{ review.review }}</p>
        </li>
      </ul>
    </div>

    <product-review v-show="selectedTab === 'Make a Review'" />
    <!-- Listening for DOM event addReview method in ProductReview.vue, which is $emitting to review-submitted and passing the item's review object here in the parent -->
  </div>
</template>

<script>
import ProductReview from "@/components/ProductReview.vue";

export default {
  name: "product-tabs",
  components: {
    ProductReview
  },
  props: {
    reviews: Array
  },
  data() {
    return {
      tabs: ["Reviews", "Make a Review"],
      selectedTab: "Reviews"
    };
  }
};
</script>

<style scoped>
.tab {
  margin: 1em;
}
</style>