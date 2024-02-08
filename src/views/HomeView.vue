<template>
  <div class="home">
    <NavbarView />
    <div class="container">
      <HeroView />
      <div class="row mt-4">
        <div class="col">
          <h2>Best <strong>Foods</strong></h2>
        </div>
        <div class="col-3 ">
          <router-link class="btn btn-warning float right" to="/foods"><b-icon-eye-fill></b-icon-eye-fill>Lihat Selengkapnya</router-link>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import NavbarView from "../components/Navbar.vue";
import HeroView from "../components/HeroView.vue";

export default {
  name: "HomeView",
  components: {
    NavbarView,
    HeroView,
  },
};
</script>
