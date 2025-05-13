<template>
  <footer class="app-footer">
    <div class="container">
      <p v-if="cartItems === 0">
        Keranjang masih kosong nih, yuk checkout.
      </p>
      <p v-else>
        {{ cartItems }} produk sudah dikeranjang, 
        <button @click="lanjutBayar" class="btn-bayar">Lanjut Bayar</button>
      </p>
    </div>
  </footer>
</template>
<script setup>
import { defineProps } from 'vue';

const props = defineProps({
  cartItems: {
    type: Number,
    default: 0,
  },
});
</script>

<style scoped>
.app-footer {
  position: fixed;
  bottom: 0;
  left: 0;
  width: 100%;
  background-color: #333;
  color: white;
  padding: 10px;
  text-align: center;
}

.container {
  display: flex;
  justify-content: center;
  align-items: center;
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 1rem;
}

.footer-links {
  display: flex;
  gap: 1rem;
}

.footer-links a {
  color: white;
  text-decoration: none;
}

.footer-links a:hover {
  text-decoration: underline;
}

.btn-bayar {
  background-color: #4CAF50; /* Warna hijau */
  color: white;
  padding: 5px 10px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-size: 16px;
}

.btn-bayar:hover {
  background-color: #45a049; /* Efek hover */
}
</style>