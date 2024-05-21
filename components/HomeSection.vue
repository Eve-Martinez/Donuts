<template>
  <v-container class="home-section home" fluid>
    <v-row align="center" justify="space-between">
      <v-col cols="12" md="6">
        <div class="text-container">
          <h1>Rápidas, frescas,</h1>
          <h2>¡& siempre deliciosas!</h2>
          <p>
            Tu destino para donas frescas y deliciosas en tiempo récord. Desde las clásicas glaseadas hasta las más innovadoras combinaciones, estamos aquí para satisfacer tus antojos más dulces en el momento que las necesitas.
          </p>
          <v-btn class="order-button" @click="scrollToSection('products')">{{ buttonText }}</v-btn>
        </div>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      buttonText: 'Ver Ahora',
    };
  },
  methods: {
    scrollToSection(sectionId) {
      document.getElementById(sectionId).scrollIntoView({ behavior: 'smooth' });
    },
  },
};
</script>

<style scoped src="@/assets/home-section.css"></style>
