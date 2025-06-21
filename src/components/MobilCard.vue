<template>
  <div class="col-md-4 mb-3">
    <div class="card">
      <div class="card-body">
        <h5>{{ mobil.nama }}</h5>
        <p>Harga: Rp {{ mobil.harga }}</p>
        <p v-if="mobil.tersedia">Tersedia</p>
        <p v-else class="text-danger">Tidak Tersedia</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["mobil"],
};
</script>
