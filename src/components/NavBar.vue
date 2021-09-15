<template>
  <nav class="main-nav">
    <router-link :to="{ name: 'Home' }">Projects</router-link>
    <router-link :to="{ name: 'AddProject' }">Add New Project</router-link>
  </nav>
</template>
<script>
export default {};
</script>
<style>
.main-nav {
  font-family: Poppins, sans-serif;
  text-align: center;
  margin: 70px auto;
  font-weight: 300;
}
.main-nav a {
  display: inline-block;
  text-decoration: none;
  margin: 0 10px;
  color: #f14f51;
  font-size: 22px;
}
a.router-link-active {
  border-bottom: 2px solid #1de9b6;
  padding-bottom: 4px;
}
</style>
