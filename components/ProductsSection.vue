<template>
  <div>
    <div class="title" id="products">
      <span class="titulo-text">Latest</span>
      <span class="subtitulo-text" :style="{ marginLeft: '1rem' }">Products</span>
    </div>
    <v-container grid-list-xl>
      <v-layout row wrap>
        <v-flex xs6 sm4 md3 v-for="(item, index) in products" :key="index">
          <v-card class="elevate-on-hover">
            <v-img :src="item.urlImg"></v-img>
            <v-card-title>
              <h2>{{ item.name }}</h2>
            </v-card-title>
            <v-card-text>
              <p style="font-size: 1.4rem; color: #e84393">${{ item.price }}</p>
            </v-card-text>
          </v-card>
        </v-flex>
      </v-layout>
    </v-container>
  </div>
</template>

<script>
export default {
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
    };
  },
};
</script>

<style scoped src="@/assets/products-section.css"></style>
