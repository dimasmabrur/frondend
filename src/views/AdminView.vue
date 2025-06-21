<template>
  <div class="container mt-4">
    <h2>Kelola Mobil</h2>
    <MobilForm @refresh="getData" :editMobil="selected" />
    <table class="table mt-3">
      <thead>
        <tr>
          <th>Nama</th>
          <th>Harga</th>
          <th>Status</th>
          <th>Aksi</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="mobil in mobils" :key="mobil.id">
          <td>{{ mobil.nama }}</td>
          <td>{{ mobil.harga }}</td>
          <td>{{ mobil.tersedia ? "Tersedia" : "Tidak" }}</td>
          <td>
            <button class="btn btn-warning btn-sm" @click="edit(mobil)">Edit</button>
            <button class="btn btn-danger btn-sm" @click="hapus(mobil.id)">Hapus</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import MobilForm from "../components/MobilForm.vue";

export default {
  components: { MobilForm },
  data() {
    return {
      mobils: [],
      selected: null,
    };
  },
  methods: {
    async getData() {
      const res = await fetch("https://rental-backend.<subdomain>.workers.dev/mobil");
      this.mobils = await res.json();
    },
    edit(mobil) {
      this.selected = mobil;
    },
    async hapus(id) {
      await fetch(`https://rental-backend.<subdomain>.workers.dev/mobil/${id}`, {
        method: "DELETE",
      });
      this.getData();
    },
  },
  mounted() {
    this.getData();
  },
};
</script>
