<template>
  <div>
    <div id="home">
      <HomeSection />
    </div>
    <div id="products">
      <ProductsSection :products="products" />
    </div>
    <div id="reviews">
      <ReviewsSection :comments="comments" @add-comment="addComment" @delete-comment="deleteComment" />
    </div>
    <div id="networks">
      <NetworksSection :platforms="platforms" />
    </div>
  </div>
</template>

<script>
import HomeSection from '~/components/HomeSection.vue';
import ProductsSection from '~/components/ProductsSection.vue';
import ReviewsSection from '~/components/ReviewsSection.vue';
import NetworksSection from '~/components/NetworksSection.vue';

export default {
  components: {
    HomeSection,
    ProductsSection,
    ReviewsSection,
    NetworksSection,
  },
};
</script>

<style src="~/assets/global.css"></style>