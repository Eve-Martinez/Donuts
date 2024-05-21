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
  props: {
    products: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style scoped src="@/assets/products-section.css"></style>
