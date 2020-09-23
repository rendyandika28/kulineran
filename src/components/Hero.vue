<template>
  <div class="row align-items-center mt-3 text-center text-md-left">
    <div class="col-md-6 hero-text">
      <h2>
        <strong>Delicious Foods Menu</strong>
        <br />In Your Gadget
      </h2>
      <p>Ayo segera pilih dan pesan makanan favorit anda</p>
      <router-link to="/foods">
        <button class="btn btn-lg btn-warning d-flex align-items-center cta">
          <b-icon-arrow-right class="mr-2"></b-icon-arrow-right>Pesan
        </button>
      </router-link>
    </div>
    <div class="col-md-6 hero-image">
      <img src="@/assets/images/hero.png" alt="hero-image" width="100%" />
    </div>
  </div>
</template>

<script>
export default {
  name: "Hero",
};
</script>

<style>
@media (max-width: 767.98px) {
  .hero-image {
    order: 1;
    margin-bottom: 20px;
  }

  .hero-text {
    order: 2;
  }

  .cta {
    margin: auto;
  }
}
</style>