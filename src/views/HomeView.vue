<template>
  <div class="container mt-4">
    <h2>Daftar Mobil</h2>
    <div class="row">
      <MobilCard v-for="mobil in mobils" :key="mobil.id" :mobil="mobil" />
    </div>
  </div>
</template>

<script>
import MobilCard from "../components/MobilCard.vue";

export default {
  components: { MobilCard },
  data() {
    return { mobils: [] };
  },
  async mounted() {
    const res = await fetch("https://rental-backend.<subdomain>.workers.dev/mobil");
    this.mobils = await res.json();
  },
};
</script>
