<template>
  <div>
    <ul>
      <li v-for="product in products" :key="product.id">
        {{ product.name }}

        <button type="button" @click="addProductToCart(product)">
          Lägg till produkt till varukorgen!
        </button>
      </li>
    </ul>

    <ul>
      <li v-for="(item, index) in cart" :key="index">
        {{ item.name }}

        <button type="button" @click="deleteProductInCart(item.id)">
          Ta bort produkt från varukorgen!
        </button>
      </li>
    </ul>
  </div>
</template>

<script>
import ProductService from "@/core/ProductService.js";
import CartService from "@/core/CartService.js";

export default {
  name: "Home",
  created() {
    this.getProducts();
    this.getCart();
  },
  data() {
    return {
      products: [],
      cart: [],
    };
  },
  methods: {
    getProducts() {
      ProductService.getProducts().then((data) => (this.products = data.data));
    },
    getCart() {
      CartService.getCart().then((data) => (this.cart = data.data));
    },
    addProductToCart(product) {
      CartService.addProductToCart(product).then(() => this.getCart());
    },
    deleteProductInCart(id) {
      CartService.deleteProductInCart(id).then(() => this.getCart());
    },
  },
};
</script>
