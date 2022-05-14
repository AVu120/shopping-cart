<script setup lang="ts"></script>

<template>
  <div class="container">
    <img class="product_image" src="/socks_green.jpeg" />
    <div class="product_info">
      <h1>Socks</h1>
      <p>In Stock</p>
    </div>
  </div>
</template>

<style>
@import "@/assets/base.css";

.container {
  display: flex;
  justify-content: center;
  height: 100vh;
  padding-top: 5rem;
}

.product_image {
  height: 300px;
  width: 300px;
}

.product_info {
  display: flex;
  flex-direction: column;
}
</style>
