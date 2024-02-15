<template>
  <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
    <div class="container">
      <router-link class="navbar-brand" to="/">Kulineran</router-link>
      <button
        class="navbar-toggler"
        type="button"
        data-toggle="collapse"
        data-target="#navbarSupportedContent"
        aria-controls="navbarSupportedContent"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav">
          <li class="nav-item">
            <router-link class="nav-link" to="/">Home</router-link>
          </li>
          <li class="nav-item">
            <router-link class="nav-link" to="/foods">Foods</router-link>
          </li>
        </ul>

        <ul class="ml-auto navbar-nav">
          <li>
            <router-link class="nav-link" to="/cart">
              Keranjang
              <b-icon-cart></b-icon-cart>
              <span class="badge badge-warning">{{updateKeranjang ? updateKeranjang.length : jumlah_pesanan.length}}</span>
            </router-link>
          </li>
        </ul>
      </div>
    </div>
  </nav>
</template>

<script>
import axios from 'axios';


export default {
  name: "NavbarView",
  data(){
    return {
      jumlah_pesanan: []
    }
  },
  props: ['updateKeranjang'],
  methods:{
    setJumlah(data) {
      this.jumlah_pesanan = data
    }
  },mounted(){
    axios
      .get("http://localhost:3000/keranjangs")
      .then((response) => this.setJumlah(response.data))
      .catch((error) => console.log(error))
  }
};
</script>

<style></style>
