<template>
  <div class="card shadow" style="width: 18rem">
    <img :src="'/img/' + product.gambar" class="card-img-top" alt="..." />
    <div class="card-body">
      <h5 class="card-title">{{product.nama}}</h5>
      <p class="card-text">
        Harga :  {{product.harga}}
      </p>
      <router-link :to="'/foods/' + product.id" class="btn btn-warning"><b-icon-bell-fill class="mr-2"></b-icon-bell-fill>Pesan Sekarang</router-link>
    </div>
  </div>
</template>

<script>
export default {
  name: "CardProduct",
  props: ["product"],
};
</script>

<style></style>
