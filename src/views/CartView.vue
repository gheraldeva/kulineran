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

      <div class="row justify-content-end">
        <div class="col-md-4">
          <form v-on:submit.prevent>
            <div class="form-group mt-3">
              <label for="nama">Nama</label>
              <input type="text" class="form-control" v-model="pesanan.nama" />
            </div>
            <div class="form-group mt-3">
              <label for="noMeja">No Meja</label>
              <input
                type="number"
                class="form-control"
                v-model="pesanan.noMeja"
              />
            </div>

            <button
              type="submit"
              class="btn btn-warning float-right"
              @click="checkout"
            >
              <b-icon-bell-fill></b-icon-bell-fill>Pesan
            </button>
          </form>
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
      keranjangs: {},
      pesanan: {},
      product:[]
    };
  },
  props: ["updatePage"],
  methods: {
    setKeranjangs(data) {
      this.keranjangs = data;
    },
    hapusKeranjang(id) {
      console.log(id);
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
    checkout() {
      if (this.pesanan.nama && this.pesanan.noMeja) {

        axios
          .post("http://localhost:3000/product_checkout/", this.keranjangs)
          .then(() => {
            this.keranjangs.map(async (item) => {
              console.log(item);
              console.log(item.id);
              try {
                return await axios
                  .delete("http://localhost:3000/keranjangs/"+item.id);
              } catch(err) {
                return console.log(err);
              }
            });

            this.$router.push({ path: "/pesanan-sukses" });
            this.$toast.success("Sukses Dipesan", {
              type: "success",
              position: "top-right",
              duration: 3000,
              dismissable: true,
            });
          })
          .catch((err) => console.log(err));
        this.product.products = this.pesanan
        axios
          .post("http://localhost:3000/pesanans/", this.product.products)
      } else {
        this.$toast.error("Nama dan No. Meja Harus diisi", {
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
