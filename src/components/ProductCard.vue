<script setup lang="ts">
interface Props {
  title: string;
  inventory: number;
  onSale: boolean;
  details: string[];
  variants: string[];
  sizes: string[];
  cart: number;
  incrementCart: () => void;
}

defineProps<Props>();
</script>

<template>
  <div class="card">
    <img class="product_image" src="/socks_green.jpeg" />
    <div class="product_info">
      <h1>{{ title + (onSale ? " - On Sale" : "") }}</h1>
      <div class="product_in_stock">
        <p v-if="inventory > 10">In Stock</p>
        <p v-else-if="inventory > 0">Almost sold out!</p>
        <p v-else>Out of Stock</p>
      </div>
      <div class="product_info_grid">
        <div>
          <h2>Details</h2>
          <!-- <ul> -->
          <li v-for="detail in details" :key="detail">{{ detail }}</li>
          <!-- </ul> -->
        </div>
        <div>
          <h2>Color</h2>
          <!-- <ul> -->
          <li v-for="variant in variants" :key="variant">{{ variant }}</li>
          <!-- </ul> -->
        </div>
        <div>
          <h2>Size</h2>
          <li v-for="size in sizes" :key="size">{{ size }}</li>
        </div>
      </div>
      <button class="add_to_cart_button" v-on:click="incrementCart()">
        Add to cart
      </button>
    </div>
  </div>
</template>

<style>
.card {
  height: 400px;
  background-color: lightblue;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 2rem;
  border-radius: 2rem;
}
.product_image {
  height: 300px;
  width: 300px;
  border: 1px solid grey;
  border-radius: 1rem;
  margin-right: 2rem;
}

.product_info {
  display: flex;
  flex-direction: column;
}

.product_in_stock {
  margin-bottom: 1rem;
}

.product_info_grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-column-gap: 1rem;
}

.add_to_cart_button {
  padding: 1rem;
  width: fit-content;
  background-color: black;
  color: white;
  border: none;
  border-radius: 1rem;
  font-weight: bold;
  cursor: pointer;
}
</style>
