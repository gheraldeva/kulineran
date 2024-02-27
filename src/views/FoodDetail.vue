<template>
  <div class="food-detail">
    <NavbarView />

    <div class="container">
      <div class="row">
        <div class="col mt-3">
          <nav aria-label="breadcrumb">
            <ol class="breadcrumb">
              <li class="breadcrumb-item">
                <router-link class="text-dark" to="/">Home</router-link>
              </li>
              <li class="breadcrumb-item">
                <router-link class="text-dark" to="/foods">Foods</router-link>
              </li>
              <li class="breadcrumb-item active" aria-current="page">
                Food Order
              </li>
            </ol>
          </nav>
        </div>
      </div>

      <div class="row">
        <div class="col-md-6">
          <img :src="'../img/' + product.gambar" class="img-fluid shadow" />
        </div>
        <div class="col-md-6">
          <h2>
            <strong>{{ product.nama }}</strong>
          </h2>
          <hr />
          <h4>
            Harga : <strong>Rp. {{ product.harga }}</strong>
          </h4>
          <form v-on:submit.prevent>
            <div class="form-group mt-3">
              <label for="jumlah_pesan">Jumlah Pesanan</label>
              <input
                type="number"
                class="form-control"
                v-model="pesanan.jumlah_pesan"
              />
            </div>
            <div class="form-group">
              <label for="Keterangan">Keterangan</label>
              <textarea
                placeholder="keterangan"
                class="form-control"
                v-model="pesanan.keterangan"
              ></textarea>
            </div>

            <button type="submit" class="btn btn-warning" @click="pemesanan">
              <b-icon-bell-fill></b-icon-bell-fill>Pesan
            </button>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import NavbarView from "../components/Navbar.vue";

export default {
  name: "FoodDetail",
  components: {
    NavbarView,
  },
  data() {
    return {
      product: {},
      pesanan: {},
    };
  },
  methods: {
    setProducts(data) {
      this.product = data;
    },
    pemesanan() {
      if (this.pesanan.jumlah_pesan) {
        this.pesanan.products = this.product;
        console.log(this.pesanan)
        axios({
          method: "POST",
          headers: {
            "Content-Type": "application/json; charset=utf-8",
          },
          url: "http://localhost:3000/keranjangs",
          data: this.pesanan,
        })
          .then(() => {
            this.$router.push({ path :"/cart" })
            this.$toast.success("Sukses Dimasukkan Keranjang", {
              type: "success",
              position: "top-right",
              duration: 3000,
              dismissable: true,
            });
          })
          .catch((error) => {
            console.log(error);
          });
      }
      else{
        this.$toast.error("Jumlah Harus Diisi ya Dek", {
              type: "error",
              position: "top-right",
              duration: 3000,
              dismissable: true,
            });
      }
      
    },
  },
  mounted() {
    axios
      .get(
        "http://localhost:3000/products/" +
          this.$route.params.id
      )
      .then((response) => {
        this.setProducts(response.data);
      })
      .catch((error) => {
        console.log("Error : " + error);
      });
  },
};
</script>

<style></style>
