<template>
  <div class="pesanan-sukses">
    <Navbar />
    <div class="container">
      <div class="row justify-content-center mt-5">
        <div class="col text-center">
          <img src="/img/undraw_Cooking_p7m1.png/" alt="" width="250" />
          <h2><strong>Pesanan Sukses Dipesan</strong></h2>
          <h6>Mohon Menunggu Pesanan Anda Selesai</h6>
        </div>
      </div>
      <div class="row">
        <div class="col text-center">
          <router-link to="/" class="btn btn-warning"><b-icon-arrow-left-circle-fill class="mr-1"></b-icon-arrow-left-circle-fill> Kembali ke Halaman Utama</router-link>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Navbar from "@/components/Navbar.vue";

export default {
  name: "PesananSukses",
  components: { Navbar },
};
</script>

<style></style>
