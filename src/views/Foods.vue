<template>
  <div class="">
    <NavbarView />

    <div class="container">
      <div class="row mt-3">
        <div class="col">
          <h2>Daftar Makanan</h2>
        </div>
      </div>

      <div class="row mt-3">
        <div class="col-12">
          <div class="input-group mb-3">
            <input
              v-model="search"
              @keyup="searchProduct"
              type="text"
              class="form-control"
              placeholder="Cari Makanan"
              aria-label="Cari"
              aria-describedby="basic-addon1"
            />
            <div class="input-group-prepend">
              <span class="input-group-text" id="basic-addon1"
                ><b-icon-search></b-icon-search
              ></span>
            </div>
          </div>
        </div>
      </div>

      <div class="row mt-3 mb-3">
        <div
          class="col-md-4 d-flex justify-content-center"
          v-for="product in products"
          :key="product.id"
        >
          <CardProduct :product="product" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import NavbarView from "../components/Navbar.vue";
import CardProduct from "../components/CardProduct.vue";
import axios from "axios";

export default {
  name: "FoodsView",
  components: {
    NavbarView,
    CardProduct,
  },
  data() {
    return {
      products: [],
      search : ''
    };
  },
  methods: {
    setProducts(data) {
      this.products = data;
    },
    searchProduct() {
      axios
        .get("https://my-json-server.typicode.com/gheraldeva/product_kulineran/products?q=" + this.search)
        .then((response) => {
          this.setProducts(response.data);
        })
        .catch((error) => {
          console.log("Error : " + error);
        });
    },
  },
  mounted() {
    axios
      .get(
        "https://my-json-server.typicode.com/gheraldeva/product_kulineran/products"
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
