<template>
<main>
  <!-- Card Start -->
 <div 
  class="card" 
  v-for="(product, index) in products" 
  :key="index"
>
  <div class="parent-img">
    <img 
      :src="product.image" 
      :alt="product.name" 
      class="img"
    />
  </div>

  <div class="text-content">
    <div>
      <h3 class="product">{{ product.name }}</h3>
      <p class="price">{{ product.price }}</p>
    </div>
    <div>
      <button @click="tambahKeKeranjang(product)" class="checkout">
        <i class="fa-solid fa-cart-shopping"></i> Checkout
      </button>
    </div>
  </div>
</div>

  <!-- Card End -->

</main>
</template>

<script setup>
import { ref } from 'vue'

// Tambahkan ini:
const emit = defineEmits(['update-cart'])

const cartCount = ref(0)
const tambahKeKeranjang = (product) => {
  cartCount.value++;

  // Emit ke App.vue, kirim produk yang ditambahkan
  emit('update-cart', {
    count: cartCount.value,
    product, // Langsung kirim produk
  });

  console.log("Produk ditambahkan ke keranjang:", product);
};
const products = [
  { 
    name: "Pecel Lele Kriuk", 
    price: "Rp 30.000", 
    image: "https://asset.kompas.com/crops/vhkkKrYsJtPGU9jIpuht1703nLs=/0x0:1000x667/1200x800/data/photo/2021/03/21/60569b33a2b3d.jpeg" 
  },
  { 
    name: "Cumi Bakar Pedas", 
    price: "Rp 45.000", 
    image: "https://www.foto.arahkita.com/2019/03/09/520-cumi_bakar_mommyasia.jpeg" 
  },
  { 
    name: "Sop Iga Bakar", 
    price: "Rp 48.000", 
    image: "https://img-global.cpcdn.com/recipes/8b4b21dd6c86cb40/680x964f0.515942_0.5_1.0q70/sop-iga-bakar-foto-resep-utama.webp" 
  },
  { 
    name: "Kepiting Pedas Manis", 
    price: "Rp 80.000", 
    image: "https://www.rakyatsulbar.com/wp-content/uploads/2024/11/main-header.jpg" 
  },
  { 
    name: "Kerang Cabai Hijau", 
    price: "Rp 25.000", 
    image: "https://asset.kompas.com/crops/6PzPU64j_PRin1U7T8rPKzh46zU=/0x0:780x520/1200x800/data/photo/2020/10/15/5f8870913dc54.jpg" 
  },
  { 
    name: "Ikan Nila Pedas Gurih", 
    price: "Rp 45.000", 
    image: "https://asset.kompas.com/crops/nI77SyYGlKeQ4bqBnPheCRU2KjQ=/23x14:673x447/1200x800/data/photo/2021/01/13/5ffe2d862876e.jpg" 
  },
];


</script>

<style scoped>
main {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  height: 800px;
  min-height: 100vh; /* Ganti height fixed */
  padding: 20px;
  margin-top: 80px;
}

.card {
  flex: 0 0 calc(25% - 30px); /* 4 kartu per baris, kurangi sedikit untuk gap */
  background: #f0f0f0;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.5);
  margin: 30px 20px 20px 20px;
}

.parent-img{
  display: flex;
  justify-content: center;
}
.img {
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.5);
  border-radius: 3%;
  background-size: cover;
  transition: 0.5s;
    width: 300px;
  height: 200px;
  max-height: 300px;
  object-fit: cover;
}

.img:hover {
 transform: scale(1.2);
 transition: 0.5s;
}

.text-content {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-top: 20px;
  padding: 10px 10px;
  background-color: bisque;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.5);
  border-radius: 10px;
}

.checkout {
  padding: 5px 20px;
  font-size: 15px;
  font-family: 'Poppins', sans-serif;
  border-radius: 999px;
  background-color: yellowgreen;
  color: rgb(103, 2, 2);
  transition: 0.5s;
}

.checkout:hover {
  color: black;
  background-color: rgb(186, 238, 53);
  transition: 0.5s;
}

@media (max-width: 1024px) {
  .card {
    flex: 0 0 calc(33.33% - 20px);
  }
}

@media (max-width: 768px) {
  .card {
    flex: 0 0 calc(50% - 20px);
  }
}
</style>