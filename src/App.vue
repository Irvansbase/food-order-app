<template>
  <div class="app">
    <NavBar @toggle-cart="toggleCartVisibility" :cartItems="cartCount" />
    <OrderList @update-cart="updateCart" />

    <div v-if="isCartVisible" class="cart-modal">
      <h2>Keranjang Belanja</h2>
      <ul>
        <li v-for="(product, index) in cartProducts" :key="index">
          <div class="product-item">
            <img :src="product.image" alt="" width="50">
            <div class="product-details">
              <p>{{ product.name }} <span class="quantity">x{{ product.quantity }}</span></p>
              <p>{{ product.price }}</p>
            </div>
            <button @click="removeFromCart(product)" class="btn-remove">X</button>
          </div>
        </li>
      </ul>
    </div>

    <AppFooter :cartItems="cartCount" />
  </div>
</template>

<script>
import NavBar from './components/navbar.vue';
import OrderList from './components/OrderList.vue';
import AppFooter from './components/AppFooter.vue';

export default {
  name: 'App',
  components: {
    NavBar,
    OrderList,
    AppFooter
  },
  data() {
    return {
      cartCount: 0,
      cartProducts: [],
      isCartVisible: false
    };
  },
  methods: {
    updateCart({ count, product }) {
      this.cartCount += 1;

      // Cek jika produk sudah ada di keranjang
      const found = this.cartProducts.find(p => p.name === product.name);

      if (found) {
        found.quantity += 1; // Jika sudah ada, tambahkan quantity
      } else {
        product.quantity = 1; // Jika belum ada, set quantity jadi 1
        this.cartProducts.push(product);
      }

      console.log("Produk di keranjang:", this.cartProducts);
    },
    toggleCartVisibility() {
      this.isCartVisible = !this.isCartVisible;
    },
    removeFromCart(product) {
      const index = this.cartProducts.findIndex(p => p.name === product.name);

      if (index !== -1) {
        if (this.cartProducts[index].quantity > 1) {
          this.cartProducts[index].quantity -= 1;
        } else {
          this.cartProducts.splice(index, 1);
        }
        this.cartCount -= 1;
      }
    }
  }
};
</script>


<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'Poppins', sans-serif;
  line-height: 1.6;
  color: #333;
}

.app {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

.cart-modal {
  position: absolute;
  right: 20px;
  top: 60px;
  background: white;
  border: 1px solid #ccc;
  padding: 10px;
  z-index: 10;
  width: 300px;
  transition: 0.5s;
}
.product-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 5px;
}
.product-details {
  flex: 1;
  margin-left: 10px;
}
.btn-remove {
  background-color: red;
  color: white;
  border: none;
  cursor: pointer;
  padding: 3px 8px;
  border-radius: 4px;
}
.btn-remove:hover {
  background-color: darkred;
}
.quantity {
  font-weight: bold;
  margin-left: 5px;
  color: #555;
}

/* Mobile S (320px - 480px) */
@media only screen and (max-width: 480px) {
  .cart-modal {
    width: 100%;
    right: 0;
    top: 60px;
    border-radius: 0;
  }
  .product-item {
    flex-direction: column;
    align-items: flex-start;
  }
  .product-details {
    margin-left: 0;
    margin-top: 5px;
  }
  .btn-remove {
    width: 100%;
    margin-top: 5px;
  }
}

/* Mobile M (481px - 767px) */
@media only screen and (max-width: 767px) {
  .cart-modal {
    width: 90%;
    right: 5%;
    top: 60px;
  }
  .product-item {
    flex-direction: column;
    align-items: flex-start;
  }
  .product-details {
    margin-left: 0;
    margin-top: 5px;
  }
}

/* Tablet (768px - 1024px) */
@media only screen and (max-width: 1024px) {
  .cart-modal {
    width: 400px;
  }
}

/* Desktop (1025px - 1200px) */
@media only screen and (max-width: 1200px) {
  .cart-modal {
    width: 350px;
  }
}

/* Large Screen (1200px and above) */
@media only screen and (min-width: 1200px) {
  .cart-modal {
    width: 300px;
  }
}

</style>