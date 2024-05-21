<template>
  <div>
    <div class="title" id="networks">
      <span class="titulo-text">Social</span>
      <span class="subtitulo-text" :style="{ marginLeft: '1rem' }">Networks</span>
    </div>
    <v-container grid-list-xl>
      <v-layout row wrap>
        <v-flex md4 v-for="(platform, index) in platforms" :key="index">
          <v-card class="elevate-on-hover">
            <v-img :src="platform.urlImg" aspect-ratio="1"></v-img>
            <v-card-title>{{ platform.name }}</v-card-title>
            <v-card-text>{{ platform.displayName }}</v-card-text>
            <v-btn :href="platform.link" target="_blank">Visit</v-btn>
          </v-card>
        </v-flex>
      </v-layout>
    </v-container>
  </div>
</template>

<script>
export default {
  props: {
    platforms: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style scoped src="@/assets/networks-section.css"></style>
