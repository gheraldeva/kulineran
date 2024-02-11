<template>
  <div class="hero">
    <!-- Desktop -->
    <div class="d-none d-md-block">
      <div class="row mt-3">
        <div class="col">
          <div class="d-flex h-100">
            <div class="justify-content-center align-self-center">
              <h2><strong>Delicious Food Menu,</strong><br />in Your Gadget</h2>
              <p>Ayo Pesan Makanan Anda!!</p>
              <router-link to="/foods" class="btn btn-warning">
                <b-icon-bell></b-icon-bell> Pesan
              </router-link>
            </div>
          </div>
        </div>
        <div class="col">
          <img src="../assets/img/undraw_breakfast_psiw.png" width="100%" />
        </div>
      </div>
    </div>

    <div class="d-md-none d-sm-block">
      <div class="row mt-3">
        <div class="col-md-6">
          <img src="../assets/img/undraw_breakfast_psiw.png" width="100%" />
        </div>

        <div class="col-md-6">
          <div class="d-flex h-100">
            <div class="justify-content-center align-self-center">
              <h2><strong>Delicious Food Menu,</strong><br />in Your Gadget</h2>
              <p>Ayo Pesan Makanan Anda!!</p>
              <router-link to="/foods" class="btn btn-warning">
                <b-icon-bell></b-icon-bell> Pesan
              </router-link>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "HeroView",
};
</script>

<style></style>
