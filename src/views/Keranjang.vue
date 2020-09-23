<template>
  <div class="keranjang">
    <Navbar :updateKeranjang="keranjang" />
    <div class="container">
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
              <li class="breadcrumb-item active">Keranjang</li>
            </ul>
          </nav>
        </div>
      </div>

      <div class="row mt-3">
        <div class="col">
          <h2>
            keranjang
            <strong>Saya</strong>
          </h2>
          <div class="table-responsive mt-5">
            <table class="table" v-if="keranjang.length">
              <thead>
                <tr>
                  <th scope="col">#</th>
                  <th scope="col">Foto</th>
                  <th scope="col">Nama Makanan</th>
                  <th scope="col">Keterangan</th>
                  <th scope="col">Jumlah</th>
                  <th scope="col">Harga</th>
                  <th scope="col">Total Harga</th>
                  <th scope="col">Aksi</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="(cart, i) in keranjang" :key="cart.id">
                  <th scope="row">{{i + 1}}</th>
                  <td>
                    <img
                      class="img-fluid"
                      width="200"
                      :src="'assets/images/' + cart.product.gambar "
                      :alt="cart.id"
                    />
                  </td>
                  <td>{{cart.product.nama}}</td>
                  <td>{{cart.keterangan ? cart.keterangan : ''}}</td>
                  <td>{{cart.jumlah_pemesanan}}</td>
                  <td>
                    Rp.
                    {{cart.product.harga}}
                  </td>
                  <td>
                    Rp.
                    <strong>{{totalHargaItem(cart.jumlah_pemesanan, cart.product.harga)}}</strong>
                  </td>
                  <td class="text-center text-danger" @click="hapusItem(cart.id)">
                    <b-icon-trash></b-icon-trash>
                  </td>
                </tr>

                <tr v-show="keranjang.length">
                  <td colspan="6" align="right">
                    <strong>Total Harga :</strong>
                  </td>
                  <td>Rp. {{totalHarga}}</td>
                </tr>
              </tbody>
            </table>
            <p v-else class="text-danger">
              Keranjang Kosong!
              <br />Tambah makanan ke keranjang
            </p>
          </div>
        </div>
      </div>

      
    </div>
  </div>
</template>

<script>
import Navbar from "@/components/Navbar.vue";
import axios from "axios";
export default {
  name: "Keranjang",
  components: {
    Navbar,
  },
  data() {
    return {
      keranjang: [],
    };
  },
  methods: {
    setKeranjang(data) {
      this.keranjang = data;
      console.log(this.keranjang);
    },
    totalHargaItem(jlh, hrg) {
      return jlh * hrg;
    },
    hapusItem(id) {
      axios
        .delete("http://localhost:3000/keranjangs/" + id)
        .then(() => {
          this.$toast.warning("Sukses Menghapus Item", {
            type: "warning",
            position: "top-right",
            duration: 3000,
            dismissible: true,
          });
          axios
            .get("http://localhost:3000/keranjangs")
            .then((res) => {
              this.setKeranjang(res.data);
            })
            .catch((err) => console.warn(err));
        })
        .catch((err) => console.warn(err));
    },
  },
  computed: {
    totalHarga() {
      return this.keranjang.reduce((item, data) => {
        return item + data.jumlah_pemesanan * data.product.harga;
      }, 0);
    },
  },
  mounted() {
    axios
      .get("http://localhost:3000/keranjangs")
      .then((res) => this.setKeranjang(res.data))
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