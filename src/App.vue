<template>
  <NavBar />
  <router-view />
  <Footer />
</template>

<script>
import NavBar from './components/NavBar.vue';
import Footer from './components/Footer.vue';
export default {
  components: { NavBar, Footer },
};
</script>

<style>
body {
  background-color: #f2f2f2;
}
#app {
  font-family: Poppins, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  max-width: 600px;
  margin: 0 auto;
  color: rgb(88, 88, 88);
}
</style>
