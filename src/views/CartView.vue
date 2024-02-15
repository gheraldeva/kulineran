<template>
  <div class="keranjang">
    <Navbar :updateKeranjang="keranjangs" />
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
                Keranjang
              </li>
            </ol>
          </nav>
        </div>
      </div>

      <div class="row">
        <div class="col">
          <h2>Keranjang <strong>Saya</strong></h2>
        </div>

        <div class="table-responsive mt-4 mx-3">
          <table class="table table-striped">
            <thead>
              <tr>
                <th scope="col">#</th>
                <th scope="col">Gambar</th>
                <th scope="col">Makanan</th>
                <th scope="col">Keterangan</th>
                <th scope="col">Jumlah</th>
                <th scope="col">Harga</th>
                <th scope="col">Total Harga</th>
                <th scope="col">Hapus</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="(item, index) in keranjangs" :key="item.id">
                <th>{{ index + 1 }}</th>
                <td>
                  <img
                    :src="'../img/' + item.products.gambar"
                    class="img-fluid shadow"
                    width="100"
                  />
                </td>
                <td>
                  <strong>{{ item.products.nama }}</strong>
                </td>
                <td>{{ item.keterangan ? item.keterangan : "-" }}</td>
                <td>{{ item.jumlah_pesan }}</td>
                <td>Rp. {{ item.products.harga }}</td>
                <td>
                  <strong>
                    Rp. {{ item.products.harga * item.jumlah_pesan }}</strong
                  >
                </td>
                <td class="text-danger" align="center">
                  <b-icon-trash @click="hapusKeranjang(item.id)"></b-icon-trash>
                </td>
              </tr>

              <tr>
                <td colspan="6" align="right">
                  <strong>Total Harga</strong>
                </td>
                <td>
                  <strong>Rp. {{ totalHarga }}</strong>
                </td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Navbar from "@/components/Navbar.vue";
import axios from "axios";

export default {
  name: "CartView",
  components: { Navbar },

  data() {
    return {
      keranjangs: [],
    };
  },
  methods: {
    setKeranjangs(data) {
      this.keranjangs = data;
    },
    hapusKeranjang(id) {
      axios
        .delete("http://localhost:3000/keranjangs/" + id)
        .then(() => {
          this.$toast.error("Sukses Dihapus", {
            type: "error",
            position: "top-right",
            duration: 3000,
            dismissable: true,
          });

          axios
            .get("http://localhost:3000/keranjangs")
            .then((response) => {
              this.setKeranjangs(response.data);
            })
            .catch((error) => {
              console.log("Error : " + error);
            });
        })
        .catch((error) => {
          console.log("Error : " + error);
        });
    },
  },
  mounted() {
    axios
      .get("http://localhost:3000/keranjangs")
      .then((response) => {
        this.setKeranjangs(response.data);
      })
      .catch((error) => {
        console.log("Error : " + error);
      });
  },
  computed: {
    totalHarga() {
      return this.keranjangs.reduce((items, data) => {
        return items + data.products.harga * data.jumlah_pesan;
      }, 0);
    },
  },
};
</script>

<style></style>
