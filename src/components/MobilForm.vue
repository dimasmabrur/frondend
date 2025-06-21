<template>
  <form @submit.prevent="submit">
    <div class="mb-2">
      <input v-model="form.nama" class="form-control" placeholder="Nama Mobil" required />
    </div>
    <div class="mb-2">
      <input
        v-model.number="form.harga"
        type="number"
        class="form-control"
        placeholder="Harga"
        required
      />
    </div>
    <div class="mb-2">
      <select v-model="form.tersedia" class="form-control">
        <option :value="true">Tersedia</option>
        <option :value="false">Tidak Tersedia</option>
      </select>
    </div>
    <button class="btn btn-primary">{{ editMobil ? "Update" : "Tambah" }}</button>
  </form>
</template>

<script>
export default {
  props: ["editMobil"],
  emits: ["refresh"],
  data() {
    return {
      form: {
        nama: "",
        harga: "",
        tersedia: true,
      },
    };
  },
  watch: {
    editMobil: {
      immediate: true,
      handler(val) {
        if (val) this.form = { ...val };
      },
    },
  },
  methods: {
    async submit() {
      const method = this.editMobil ? "PUT" : "POST";
      const url = this.editMobil
        ? `https://rental-backend.<subdomain>.workers.dev/mobil/${this.editMobil.id}`
        : `https://rental-backend.<subdomain>.workers.dev/mobil`;

      await fetch(url, {
        method,
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(this.form),
      });
      this.form = { nama: "", harga: "", tersedia: true };
      this.$emit("refresh");
    },
  },
};
</script>
