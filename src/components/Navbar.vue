<template>
  <div>
    <b-navbar toggleable="lg" type="light">
      <div class="container">
        <b-navbar-brand href="#">Kulineran</b-navbar-brand>

        <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

        <b-collapse id="nav-collapse" is-nav>
          <b-navbar-nav>
            <ul class="navbar-nav mr-auto">
              <li class="nav-item">
                <router-link class="nav-link" to="/">Home</router-link>
              </li>
              <li class="nav-item">
                <router-link class="nav-link" to="/foods">Foods</router-link>
              </li>
            </ul>
          </b-navbar-nav>

          <!-- Right aligned nav items -->
          <b-navbar-nav class="ml-auto">
            <ul class="navbar-nav ml-auto">
              <li class="nav-item">
                <router-link class="nav-link" to="/keranjang">
                  Keranjang
                  <b-icon-bag></b-icon-bag>
                  <span
                    class="badge badge-warning ml-2"
                  >{{updateKeranjang? updateKeranjang.length :pesanan.length}}</span>
                </router-link>
              </li>
            </ul>
          </b-navbar-nav>
        </b-collapse>
      </div>
    </b-navbar>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "Navbar",
  data() {
    return {
      pesanan: [],
    };
  },
  props: ["updateKeranjang"],
  methods: {
    setPesanan(data) {
      this.pesanan = data;
    },
  },
  mounted() {
    axios
      .get("http://localhost:3000/keranjangs")
      .then((res) => this.setPesanan(res.data))
      .catch((err) => console.warn(err));
  },
};
</script>

<style>
</style>