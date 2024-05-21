<template>
  <v-card class="overflow-hidden d-flex flex-column" style="height: 100vh;">
    <v-app-bar
      color="white"
      elevate-on-scroll
      scroll-target="#scrolling-techniques-7"
    >
      <v-app-bar-nav-icon v-show="isMobile" @click="toggleMenu"></v-app-bar-nav-icon>

      <v-toolbar-title>DonasExpress</v-toolbar-title>

      <v-spacer></v-spacer>

      <v-btn v-show="!isMobile" @click="scrollToSection('home')" class="mr-4 hover-pink-text">
        <span>Home</span>
      </v-btn>

      <v-btn v-show="!isMobile" @click="scrollToSection('products')" class="mr-4 hover-pink-text">
        <span>Products</span>
      </v-btn>

      <v-btn v-show="!isMobile" @click="scrollToSection('reviews')" class="mr-4 hover-pink-text">
        <span>Reviews</span>
      </v-btn>

      <v-btn v-show="!isMobile" @click="scrollToSection('networks')" class="hover-pink-text">
        <span>Networks</span>
      </v-btn>
    </v-app-bar>

    <v-navigation-drawer v-model="drawer" app temporary>
      <v-list>
        <v-list-item @click="selectSection('home')" :class="{ 'pink--text': activeSection === 'home' }">
          <v-list-item-content>Home</v-list-item-content>
        </v-list-item>

        <v-list-item @click="selectSection('products')" :class="{ 'pink--text': activeSection === 'products' }">
          <v-list-item-content>Products</v-list-item-content>
        </v-list-item>

        <v-list-item @click="selectSection('reviews')" :class="{ 'pink--text': activeSection === 'reviews' }">
          <v-list-item-content>Reviews</v-list-item-content>
        </v-list-item>

        <v-list-item @click="selectSection('networks')" :class="{ 'pink--text': activeSection === 'networks' }">
          <v-list-item-content>Networks</v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-sheet
      id="scrolling-techniques-7"
      class="d-flex flex-column overflow-y-auto"
      style="flex-grow: 1;"
    >
      <v-container fluid class="pa-0 flex-grow-1">
        <slot></slot>
      </v-container>
      <FooterSection />
    </v-sheet>
  </v-card>
</template>

<script>
import FooterSection from '~/components/FooterSection.vue';

export default {
  components: {
    FooterSection,
  },
  data() {
    return {
      isMobile: false,
      sheetHeight: '600px',
      drawer: false,
      activeSection: null,
    };
  },
  mounted() {
    this.checkIfMobile();
    window.addEventListener('resize', this.checkIfMobile);
  },
  destroyed() {
    window.removeEventListener('resize', this.checkIfMobile);
  },
  methods: {
    scrollToSection(sectionId) {
      document.getElementById(sectionId).scrollIntoView({ behavior: 'smooth' });
      this.activeSection = sectionId;
    },
    toggleMenu() {
      this.drawer = !this.drawer;
    },
    checkIfMobile() {
      this.isMobile = window.innerWidth <= 768;
      this.sheetHeight = this.isMobile ? 'auto' : '600px';
    },
    selectSection(sectionId) {
      this.scrollToSection(sectionId);
      this.drawer = false;
    },
  }
};
</script>

<style scoped src="@/assets/navbar-section.css"></style>
