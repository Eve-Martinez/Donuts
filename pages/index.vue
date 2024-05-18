<template>
  <div>
    <!-- Sección principal de la página con imagen de fondo -->
    <div class="home" id="home">
      <!-- Encabezado con título y navegación -->
    <header>
      <div class="header-top">
        <h1 style="font-size: 2rem;">DonasExpress</h1>
      </div>
      <button class="menu-button" @click="toggleMenu">
        <span :class="{ open: menuOpen }"></span>
        <span :class="{ open: menuOpen }"></span>
        <span :class="{ open: menuOpen }"></span>
      </button>
      <nav class="menu" :class="{ open: menuOpen }" ref="menu">
        <ul>
          <li><a href="#home" @click.prevent="scrollToSection('home')">Home</a></li>
          <li><a href="#products" @click.prevent="scrollToSection('products')">Products</a></li>
          <li><a href="#reviews" @click.prevent="scrollToSection('reviews')">Reviews</a></li>
          <li><a href="#networks" @click.prevent="scrollToSection('networks')">Networks</a></li>
        </ul>
      </nav>
    </header>

      <v-container grid-list-xl>
        <v-layout row wrap>
          <!-- Contenido de la página principal -->
          <v-flex xs12 md6 lg6>
            <div class="text-container">
              <h1>Rápidas, frescas,</h1>
              <h2>¡& siempre deliciosas!</h2>
              <p>
                Tu destino para donas frescas y deliciosas en tiempo récord. Desde las clásicas glaseadas hasta las más innovadoras combinaciones, estamos aquí para satisfacer tus antojos más dulces en el momento que las necesitas.
              </p>
              <button class="order-button" @click.prevent="scrollToSection('products')">{{ buttonText }}</button>
            </div>
          </v-flex>
          <!-- Logo -->
          <v-flex xs12 md6 lg6 class="logo-container">
            <img src="/logo.png" alt="Logo" class="logo">
          </v-flex>
        </v-layout>
      </v-container>
    </div>

    <!-- Sección de productos -->
    <div class="title" id="products" >
      <span class="titulo-text">Latest</span>
      <span class="subtitulo-text" :style="{ marginLeft: '1rem' }">Products</span>
    </div>
    <v-container grid-list-xl>
      <v-layout row wrap>
        <!-- Listado de productos -->
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

    <!-- Sección de comentarios -->
    <div class="title" id="reviews">
      <span class="titulo-text">Customer’s</span>
      <span class="subtitulo-text" :style="{ marginLeft: '1rem' }">Review</span>
    </div>
    <v-container grid-list-xl>
      <v-layout row wrap>
        <v-flex md6>
          <!-- Listado de comentarios -->
          <v-card v-for="(item, index) in listaComentarios" :key="index">
            <v-card-text>
              <h1 style="color: #e84393">{{item.nombre}}</h1>
              <p>{{item.descripcion}}</p>
              <v-btn class="white-text-button" color="#e84393" @click="eliminarComentario(item.id)">Eliminar</v-btn>
            </v-card-text>
          </v-card>
        </v-flex>

        <!-- Formulario para agregar comentarios -->
        <v-flex md6>
          <v-card>
            <v-form @submit.prevent="agregarComentario">
              <v-text-field label="Nombre" v-model="nombre"></v-text-field>
              <v-textarea label="Descripción" v-model="descripcion" class="align-right"></v-textarea>
              <v-btn block class="white-text-button" color="#333" type="submit">Agregar Comentario</v-btn>
            </v-form>
          </v-card>
        </v-flex>
      </v-layout>
      <v-snackbar v-model="snackbar">
        {{ mensaje }}
      </v-snackbar>
    </v-container>

    <!-- Sección de redes sociales -->
    <div class="title" id="networks">
      <span class="titulo-text">Social </span>
      <span class="subtitulo-text" :style="{ marginLeft: '1rem' }">Networks</span>
    </div>
    <div class="list">
      <div class="media" v-for="(platform, index) in platforms" :key="index">
        <v-img :src="platform.urlImg" class="platform-img"></v-img>
        <div class="media-content">
          <h2>{{ platform.name }}</h2>
          <a :href="platform.link" target="_blank" class="link">{{ platform.displayName }}</a>
        </div>
        <img src="/img.png" alt="img" class="img">
      </div>
    </div>

    <!-- Pie de página -->
    <footer class="footer" :style="{ backgroundColor: '#fff', color: '#333', padding: '1rem 0', marginTop: '2rem' }">
      <div class="footer-content" :style="{ maxWidth: '1200px', margin: '0 auto', display: 'flex', flexDirection: 'column', alignItems: 'center' }">
        <p>&copy; 2024 Aloux. All rights reserved.</p>
        <nav class="footer-nav" :style="{ marginTop: '1rem' }">
          <ul :style="{ listStyle: 'none', padding: 0, display: 'flex', gap: '1rem' }">
            <li><a href="#home" @click.prevent="scrollToSection('home')" :style="{ color: '#333', textDecoration: 'none' }">Home</a></li>
            <li><a href="#products" @click.prevent="scrollToSection('products')" :style="{ color: '#333', textDecoration: 'none' }">Products</a></li>
            <li><a href="#reviews" @click.prevent="scrollToSection('reviews')" :style="{ color: '#333', textDecoration: 'none' }">Reviews</a></li>
            <li><a href="#networks" @click.prevent="scrollToSection('networks')" :style="{ color: '#333', textDecoration: 'none' }">Networks</a></li>
          </ul>
        </nav>
      </div>
    </footer>
  </div>
</template>

<script>
export default {
  data() {
    return {
      products: [
        { urlImg: "/img/dona1.png", name: "Piña", price: 150 },
        { urlImg: "/img/dona2.png", name: "Galleta", price: 80 },
        { urlImg: "/img/dona3.png", name: "Fresa", price: 120 },
        { urlImg: "/img/dona4.png", name: "Limón", price: 180 },
        { urlImg: "/img/dona5.png", name: "Mora", price: 220 },
        { urlImg: "/img/dona6.png", name: "Almendra", price: 380 },
        { urlImg: "/img/dona7.png", name: "Uva", price: 210 },
        { urlImg: "/img/dona8.png", name: "Coco", price: 410 }
      ],
      platforms: [
        { urlImg: "/img/whatsapp.png", name: 'WhatsApp', displayName: '125-159-1598', link: 'https://wa.me/1251591598' },
        { urlImg: "/img/facebook.png", name: 'Facebook', displayName: 'DonasExpress', link: 'https://www.facebook.com/DonasExpress' },
        { urlImg: "/img/instagram.png", name: 'Instagram', displayName: 'Donas_Express01', link: 'https://www.instagram.com/Donas_Express01' },
        { urlImg: "/img/gmail.png", name: 'Gmail', displayName: 'donas.express@gmail.com', link: 'mailto:donas.express@gmail.com' }
      ],
      listaComentarios: [
        { id: 1, nombre: 'Karla', descripcion: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Quas aut quasi, porro vero officia in ipsa illo deleniti, voluptatibus, eligendi voluptatum incidunt nihil dolores obcaecati culpa ad odio corrupti harum.' },
        { id: 2, nombre: 'Alex', descripcion: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Quas aut quasi, porro vero officia in ipsa illo deleniti, voluptatibus, eligendi voluptatum incidunt nihil dolores obcaecati culpa ad odio corrupti harum.' }
      ],
      nombre: '',
      descripcion: '',
      snackbar: false,
      mensaje: '',
      buttonText: 'Ver Ahora',
      menuOpen: false,
    }
  },
  methods: {
    agregarComentario() {
      if (!this.nombre || !this.descripcion) {
        this.snackbar = true;
        this.mensaje = 'Llena todos los campos';
        return;
      }
      this.listaComentarios.push({
        id: Date.now(),
        nombre: this.nombre,
        descripcion: this.descripcion,
      });
      this.nombre = '';
      this.descripcion = '';
      this.snackbar = true;
      this.mensaje = 'Comentario agregado';
    },
    eliminarComentario(id) {
      this.listaComentarios = this.listaComentarios.filter(e => e.id !== id);
    },
    scrollToSection(sectionId) {
      document.getElementById(sectionId).scrollIntoView({ behavior: 'smooth' });
    },
    toggleMenu() {
      this.menuOpen = !this.menuOpen;
    },
  },
};
</script>

<style scoped>
html {
  scroll-behavior: smooth;
}

.home {
  height: 100vh;
  margin: 0;
  background-image: url('/home.png');
  background-position: right;
  background-size: cover;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem;
  position: relative;
}

.logo {
  position: absolute;
  right: 2rem;
  bottom: 2rem;
  width: 500px;
  height: auto;
  transition: transform 0.3s ease-in-out;
}

.img {
  top: 0;
  position: absolute;
  right: 10rem;
  bottom: 10rem;
  width: 400px;
  height: auto;
  transition: transform 0.3s ease-in-out;
}

.text-container {
  max-width: 50rem;
  padding-left: 5rem;
  margin-top: 1rem;
}

.text-container h1 {
  font-size: 4rem;
  color: #333;
}

.text-container h2 {
  font-size: 3rem;
  margin-top: 2rem;
  color: #e84393;
}

.text-container p {
  font-size: 1.5rem;
  color: #6b6b6b;
  padding: 1rem 0;
  line-height: 1.5;
}

.order-button {
  display: inline-block;
  margin-top: 2rem;
  border-radius: 5rem;
  background: #333;
  color: #fff;
  padding: 0.5rem 3rem;
  cursor: pointer;
  font-size: 1.4rem;
  transition: all 0.3s ease;
}

.order-button:hover {
  background: #e84393;
}

.title {
  background-color: #FFF5FA;
  padding: 1rem;
  margin: 3.5rem;
  justify-content: center;
  display: flex;
}

.titulo-text {
  color: #E84293;
  font-size: 45px;
  font-weight: bold;
}

.subtitulo-text {
  color: #333333;
  font-size: 45px;
  font-weight: bold;
}

.elevate-on-hover {
  transition: transform 0.3s ease-in-out;
}

.elevate-on-hover:hover {
  transform: translateY(-10px);
}

header {
  width: 100%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem 2rem;
  background-color: rgba(255, 255, 255, 0.8);
  position: fixed;
  top: 0;
  left: 0;
  z-index: 1000;
}

.header-top {
  font-size: 2rem;
  font-weight: bold;
  color: #333;
}

.menu-button {
  display: none;
  flex-direction: column;
  justify-content: space-between;
  width: 30px;
  height: 21px;
  background: transparent;
  border: none;
  cursor: pointer;
  z-index: 1100;
}

.menu-button span {
  display: block;
  height: 3px;
  width: 100%;
  background: #333;
  border-radius: 5px;
  transition: all 0.3s ease-in-out;
}

.menu-button span.open:nth-child(1) {
  transform: rotate(45deg) translateY(9px);
}

.menu-button span.open:nth-child(2) {
  opacity: 0;
}

.menu-button span.open:nth-child(3) {
  transform: rotate(-45deg) translateY(-9px);
}

nav {
  display: flex;
  flex-direction: row;
  justify-content: flex-end;
  width: auto;
}

nav ul {
  list-style-type: none;
  display: flex;
  gap: 2rem;
  margin: 0;
  padding: 0;
}

nav a {
  text-decoration: none;
  font-size: 1.2rem;
  color: #333;
  transition: color 0.3s ease;
}

nav a:hover {
  color: #e84393;
}

.list {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  position: relative;
  color: #e84393;
  font-size: 1.4rem;
}
.platform-img {
  margin-right: 30px; 
  width: 50px; 
  height: 50px; 
}
.media {
  display: flex;
  align-items: center;
  margin-bottom: 80px; 
}
.media-content {
  display: flex;
  flex-direction: column;
}
.link {
  color: #797274;
  text-decoration: none;
}
@media (min-width: 768px) {
  .media:nth-child(odd) {
    margin-left: 150px;
  }
  .media:nth-child(even) {
    margin-left: 300px;
  }
}
@media (max-width: 767px) {
  .media {
    margin-left: 0;
  }
}

@media (max-width: 992px) {
  .home {
    background-position: center;
  }
  .text-container {
    padding-left: 2rem;
  }
  .text-container h1 {
    font-size: 3rem;
  }
  .text-container h2 {
    font-size: 2.5rem;
  }
  .text-container p {
    font-size: 1.2rem;
  }
  .order-button {
    font-size: 1.2rem;
    padding: 0.4rem 2.5rem;
  }
  .logo {
    transform: scale(0.6);
  }
  .title {
    padding: 0.5rem;
    margin: 2rem;
  }
  .titulo-text, .subtitulo-text {
    font-size: 35px;
  }
}

@media (max-width: 768px) {
  .text-container {
    padding-left: 1rem;
  }
  .text-container h1 {
    font-size: 2.5rem;
  }
  .text-container h2 {
    font-size: 2rem;
  }
  .text-container p {
    font-size: 1rem;
  }
  .order-button {
    font-size: 1rem;
    padding: 0.3rem 2rem;
  }
  .logo {
    transform: scale(0.0);
  }
  .platform-img{
    margin-left: 4rem;
  }
  .media-content h2 {
    font-size: 2rem;
  }
  .media-content a {
    font-size: 1.3rem;
  }
  .img {
    transform: scale(0.7);
    left: 20rem;
    top: -2rem;
  }
  .menu-button {
    display: flex;
  }
  nav {
    flex-direction: column;
    justify-content: flex-start;
    position: fixed;
    top: 0;
    right: 0;
    height: 100%;
    width: 50%;
    background-color: rgba(255, 255, 255, 0.9);
    padding: 2rem;
    transform: translateX(100%);
    transition: transform 0.3s ease-in-out;
  }
  nav.open {
    transform: translateX(0);
  }
  nav ul {
    flex-direction: column;
    gap: 1rem;
  }
  .title {
    padding: 0.5rem;
    margin: 1.5rem;
  }
  .titulo-text, .subtitulo-text {
    font-size: 30px;
  }
}

@media (max-width: 480px) {
  .text-container {
    padding-left: 0.5rem;
  }
  .text-container h1 {
    font-size: 2rem;
  }
  .text-container h2 {
    font-size: 1.5rem;
  }
  .text-container p {
    font-size: 0.9rem;
  }
  .order-button {
    font-size: 0.8rem;
    padding: 0.3rem 1.5rem;
  }
  .logo {
    transform: scale(0.0);
  }
  .platform-img{
    margin-left: 2rem;
  }
  .media-content h2 {
    font-size: 1.5rem;
  }
  .media-content a {
    font-size: 0.9rem;
  }
  .img {
    transform: scale(0.5);
    left: 7rem;
    top: -5rem;
  }
  .title {
    padding: 0.5rem;
    margin: 1rem;
  }
  .titulo-text, .subtitulo-text {
    font-size: 25px;
  }
}
</style>
