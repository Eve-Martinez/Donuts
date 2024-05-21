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
import HomeSection from '~/components/HomeSection.vue';
import ProductsSection from '~/components/ProductsSection.vue';
import ReviewsSection from '~/components/ReviewsSection.vue';
import NetworksSection from '~/components/NetworksSection.vue';

export default {
  components: {
    NavBar,
    HomeSection,
    ProductsSection,
    ReviewsSection,
    NetworksSection,
  },
  data() {
    return {
      products: [
        { urlImg: "/img/dona1.png", name: "Piña", price: 150 },
        { urlImg: "/img/dona2.png", name: "Chocolate", price: 120 },
        { urlImg: "/img/dona3.png", name: "Fresa", price: 100 },
        { urlImg: "/img/dona4.png", name: "Limón", price: 80 },
        { urlImg: "/img/dona5.png", name: "Mora", price: 190 },
        { urlImg: "/img/dona6.png", name: "Almendra", price: 210 },
        { urlImg: "/img/dona7.png", name: "Uva", price: 250 },
        { urlImg: "/img/dona8.png", name: "Chocolate", price: 300 },
      ],
      comments: [
        { name: "Carlos", review: "Deliciosas donas, las mejores que he probado." },
        { name: "Ana", review: "Excelente servicio y sabor incomparable." }
      ],
      platforms: [
        { urlImg: "/img/whatsapp.png", name: "WhatsApp", displayName: "125-159-1598", link: "https://wa.me/1251591598" },
        { urlImg: "/img/instagram.png", name: "Instagram", displayName: "@donasexpress", link: "https://instagram.com/donasexpress" },
      ],
    };
  },
  methods: {
    addComment(newComment) {
      this.comments.push(newComment);
    },
    deleteComment(index) {
      this.comments.splice(index, 1);
    },
  },
};
</script>

<style src="~/assets/global.css"></style>
