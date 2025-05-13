<template>
  <header>
    <nav class="nav">
      <div class="brand">
        <h1 class="text-2xl font-bold">Irvans Store</h1>
      </div>
      <div class="hamburger" @click="toggleMenu">
        <i class='bx bx-menu'></i>
      </div>
      <ul :class="{'nav-list': true, 'nav-active': isMenuOpen}">
        <li><a href="#">Home</a></li>
        <li><a href="#">Product</a></li>
        <li>
          <button class="btn-cart" @click="$emit('toggle-cart')">
            <i class="fa-solid fa-cart-shopping"></i> Cart ({{ cartItems }})
          </button>
        </li>
      </ul>
    </nav>
  </header>
</template>

<script setup>
import { ref } from 'vue';
import { defineProps } from 'vue';
import 'boxicons/css/boxicons.min.css'; // Import Boxicons CSS

const props = defineProps({
  cartItems: {
    type: Number,
    default: 0,
  }
});

const isMenuOpen = ref(false);

const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value;
};

</script>

<style scooped>
header {
  background-color: green;
  box-shadow: 0 10px 15px rgba(0, 0, 0, 0.15);
  position: fixed;
  width: 100%;
  z-index: 1000;
}

.nav {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px 20px;
  color: rgb(255, 255, 255);
  max-width: 80%;
  font-family: 'Poppins', sans-serif;
  margin: 0 auto;
}

.brand {
  font-size: 20px;
  color: white;
}

.hamburger {
  display: none;
  font-size: 24px;
  color: white;
  cursor: pointer;
}

.nav-list {
  display: flex;
  justify-content: space-between;
  gap: 20px; 
  align-items: center;
  list-style: none;
}

.nav-list li {
  padding: 2px 8px; 
}

.nav-list li a {
  color: white;
  text-decoration: none;
}

.btn-cart {
  padding: 5px 20px;
  font-size: 15px;
  font-family: 'Poppins', sans-serif;
  border-radius: 10px;
  background-color: rgb(244, 255, 223);
  color: rgb(103, 2, 2);
  transition: 0.5s;
}

.btn-cart:hover {
  color: black;
  background-color: rgb(186, 238, 53);
  transition: 0.5s;
}

/* Responsive */
@media (max-width: 768px) {
  .hamburger {
    display: block;
  }
  .nav-list {
    display: none;
    position: absolute;
    top: 60px;
    right: 20px;
    background-color: green;
    flex-direction: column;
    gap: 10px;
    width: 150px;
    border-radius: 8px;
    overflow: hidden;
  }
  .nav-active {
    display: flex;
  }
}
</style>