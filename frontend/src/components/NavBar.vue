<template>
  <nav>
    <router-link to="/" class="logo-url"
      ><img :src="logo" id="logo" :alt="alt" height="26"
    /></router-link>
    <div>
      <router-link to="/">Home</router-link>
      <router-link to="/pedidos">Pedidios</router-link>
    </div>
  </nav>
</template>

<script>
export default {
  name: "Navbar",
  props: ["logo", "alt"],
};
</script>

<style scoped>
nav {
  background-color: #111;
  padding: 15px 50px;
  display: flex;
  justify-content: flex-end;
  align-items: center;
  border-bottom: 2px solid #00b050;
}

.logo-url {
  margin: auto;
  margin-left: 0;
}

nav a {
  color: #00b050;
  text-decoration: none;
  margin: 12px;
  transition: 0.5s;
  font-weight: 500px;
}

nav a:hover {
  color: white;
}
</style>