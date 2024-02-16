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
          <router-link class="btn btn-warning float right" to="/foods"><b-icon-eye-fill class="mr-2"></b-icon-eye-fill>Lihat Selengkapnya</router-link>
        </div>
      </div>

      <div class="row mt-3 mb-3">
        <div class="col-md-4" v-for="product in products" :key="product.id">
          <CardProduct :product="product"/>
        </div>
      </div>


    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import NavbarView from "../components/Navbar.vue";
import HeroView from "../components/HeroView.vue";
import CardProduct from "../components/CardProduct.vue";
import axios from 'axios'

export default {
  name: "HomeView",
  components: {
    NavbarView,
    HeroView,
    CardProduct
  },
  data() {
    return{
      products : []
    }
  }
  ,
  methods : {
    setProducts(data){
      this.products = data
    }
  },
  mounted(){
    axios
      .get("http://localhost:3000/best-products")
      .then((response) => {
        this.setProducts(response.data)
      })
      .catch((error) => {
        console.log("Error : " + error);
      })
  }
};
</script>
