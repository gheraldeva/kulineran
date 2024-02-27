<template>
  <div class="admin">
    <Navbar />
    <div class="container">
      <div
        async
        v-for="product in products"
        :key="product.id"
        :updatePage="product"
      >
        <h4 class="text-center mt-3">Pesanan : {{ product.nama }}</h4>
        <div class="row">
          <div
            class="col-4 mt-5"
            v-for="(PKeranjang, i) in PKeranjangs"
            :key="PKeranjang.id"
          >
            <div>
              <b-card
                :title="PKeranjang[i].products.nama"
                :img-src="'/img/' + PKeranjang[i].products.gambar"
                img-alt="Image"
                img-top
                tag="article"
                style="min-width: 15rem"
                class=""
              >
                <b-card-text>
                  Harga : Rp. {{ PKeranjang[i].products.harga }}
                </b-card-text>

                <b-button
                  variant="warning"
                  @click="pesananSelesai(PKeranjang.id[i])"
                  >Pesanan Selesai</b-button
                >
              </b-card>
            </div>
            <hr />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Navbar from "../components/Navbar.vue";
import axios from "axios";

export default {
  name: "AdminView",
  components: {
    Navbar,
  },
  data() {
    return {
      products: [],
      PKeranjangs: [],
    };
  },
  methods: {
    setProducts(data) {
      this.products = data;
    },
    setPKeranjangs(data) {
      this.PKeranjangs = data;
    },
    pesananSelesai(data) {
      console.log(data);
      axios({
        method: "DELETE",
        headers: {
          "Content-Type": "application/json; charset=utf-8",
        },
        url: "http://localhost:3000/product_checkout/" + data,
        data: data,
      })
        .then(() => {
          this.$toast.error("Sukses Dihapus", {
            type: "error",
            position: "top-right",
            duration: 3000,
            dismissable: true,
          });
          axios
            .get("http://localhost:3000/pesanans/")
            .then((response) => {
              this.setProducts(response.data);
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
      .get("http://localhost:3000/pesanans/")
      .then((response) => {
        this.setProducts(response.data);
      })
      .catch((error) => {
        console.log("Error : " + error);
      });


    axios
      .get("http://localhost:3000/product_checkout/")
      .then((response) => {
        this.setPKeranjangs(response.data);
      })
      .catch((error) => {
        console.log("Error : " + error);
      });
  },
};
</script>

<style></style>
