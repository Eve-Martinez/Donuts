<template>
  <v-app>
    <NavBar>
      <template v-slot:default>
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
      </template>
    </NavBar>
      <v-main>
          <Nuxt>
          </Nuxt>
      </v-main>
      <FooterSection />
  </v-app>
</template>
<script>
import NavBar from '~/components/NavBar.vue';
import FooterSection from '~/components/FooterSection.vue';
export default {
  components: {
    NavBar,
    FooterSection
  }
};
</script>
<style src="~/assets/global.css"></style>
