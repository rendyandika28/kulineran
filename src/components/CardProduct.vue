<template>
  <div class="card shadow card-product">
    <div class="card-image">
      <img :src="'assets/images/' + product.gambar" class="card-img-top" :alt="product.id" />
    </div>
    <div class="card-body">
      <h5 class="card-title">{{product.nama}}</h5>
      <p class="card-text">
        Harga:
        <strong>Rp. {{product.harga}}</strong>
      </p>
      <router-link class="btn btn-warning" :to="'/foods/' + product.id">
        <b-icon-cart></b-icon-cart>Pesan
      </router-link>
    </div>
  </div>
</template>

<script>
export default {
  name: "CardProduct",
  props: ["product"],
};
</script>

<style>
</style>
