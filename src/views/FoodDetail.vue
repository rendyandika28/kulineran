<template>
  <div class="food-detail">
    <Navbar />
    <div class="container">
      <!-- Breadcrumb -->
      <div class="row">
        <div class="col">
          <nav aria-label="breadcrumb">
            <ul class="breadcrumb">
              <li class="breadcrumb-item">
                <router-link to="/" class="text-dark">Home</router-link>
              </li>
              <li class="breadcrumb-item">
                <router-link to="/foods" class="text-dark">Foods</router-link>
              </li>
              <li class="breadcrumb-item active">Food Order</li>
            </ul>
          </nav>
        </div>
      </div>

      <div class="row">
        <div class="col-md-4">
          <img
            :src="'assets/images/' + product.gambar"
            class="img-fluid shadow rounded"
            width="400"
          />
        </div>
        <div class="col-md-8">
          <h4>
            <strong>{{product.nama}}</strong>
          </h4>
          <hr />
          <h6 class="my-4">
            Harga:
            <strong>Rp. {{product.harga}}</strong>
          </h6>
          <form @submit.prevent="pemesanan">
            <div class="form-group">
              <label for>Jumlah Pesanan</label>
              <input type="number" class="form-control" v-model="pesan.jumlah_pemesanan" />
            </div>
            <div class="form-group">
              <label for>Keterangan</label>
              <textarea
                class="form-control"
                placeholder="Keterangan tambahan"
                rows="3"
                v-model="pesan.keterangan"
              ></textarea>
            </div>
            <button type="submit" class="btn btn-warning">
              <b-icon-cart></b-icon-cart>Pesan
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
  name: "FoodDetail",
  components: {
    Navbar,
  },
  data() {
    return {
      product: {},
      pesan: {},
    };
  },
  methods: {
    setProduct(data) {
      this.product = data;
    },
    pemesanan() {
      this.pesan.product = this.product;
      if (this.pesan.jumlah_pemesanan) {
        axios
          .post("http://localhost:3000/keranjangs", this.pesan)
          .then(() => {
            this.$router.push({ path: "/keranjang" });
            this.$toast.success("Sukses masuk ke keranjang", {
              type: "success",
              position: "top-right",
              duration: 3000,
              dismissible: true,
            });

            this.pesan.jumlah_pemesanan = "";
            this.pesan.keterangan = "";
          })
          .catch((err) => console.warn(err.message));
      } else {
        this.$toast.warning("Anda Harus Memasukkan Jumlah Pesanan", {
          type: "warning",
          position: "top-right",
          duration: 3000,
          dismissible: true,
        });
      }
    },
  },
  mounted() {
    axios
      .get("http://localhost:3000/products/" + this.$route.params.id)
      .then((res) => this.setProduct(res.data))
      .catch((err) => console.warn(err));
  },
};
</script>

<style>
.breadcrumb {
  background-color: unset !important;
  margin-top: 10px;
  padding: 0;
}
.breadcrumb-item.active {
  font-weight: bold;
}
</style>