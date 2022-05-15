<script setup lang="ts">
import ProductCard from "@/components/ProductCard.vue";
import { ref } from "vue";

const inventory = ref(10);
const onSale = true;
const details = ["50% cotton", "30% wool", "20% polyester"];
const variants = [
  { color: "green", image: "/socks_green.jpeg" },
  { color: "blue", image: "/socks_blue.jpeg" },
];
const sizes = ["xs", "s", "m", "l", "xl"];
let cart = ref(0);

const addToCart = () => {
  cart.value++;
};
</script>

<template>
  <div class="container">
    <ProductCard
      title="Socks"
      :inventory="inventory"
      :on-sale="onSale"
      :details="details"
      :variants="variants"
      :sizes="sizes"
      :cart="cart"
      :add-to-cart="addToCart"
    />
    <div class="cart">Cart({{ cart }})</div>
  </div>
</template>

<style>
@import "@/assets/base.css";

.container {
  display: flex;
}

.cart {
  position: absolute;
  right: 1rem;
  border: 1px solid grey;
  border-radius: 0.5rem;
  padding: 0.5rem;
  background-color: white;
}
</style>
