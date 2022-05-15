<script setup lang="ts">
import ProductCard from "@/components/ProductCard.vue";
import ReviewForm from "@/components/ReviewForm.vue";
import Reviews from "@/components/Reviews.vue";
import { ref } from "vue";
import type { IReview } from "@/types";

const inventory = ref(1);
const onSale = true;
const details = ["50% cotton", "30% wool", "20% polyester"];
const variants = [
  { color: "green", image: "/socks_green.jpeg" },
  { color: "blue", image: "/socks_blue.jpeg" },
];
const sizes = ["xs", "s", "m", "l", "xl"];
let cart = ref(0);
const reviews = ref<IReview[]>([]);

const addToCart = () => {
  cart.value++;
};

const removeFromCart = () => {
  cart.value > 0 && cart.value--;
};

const submitReview = ({ name, review, rating }: IReview) => {
  reviews.value.push({ name, review, rating });
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
      :remove-from-cart="removeFromCart"
    />
    <div class="cart">Cart({{ cart }})</div>
    <div class="review_section">
      <ReviewForm :onSubmit="submitReview" />
      <Reviews :reviews="reviews" />
    </div>
  </div>
</template>

<style>
@import "@/assets/base.css";

.container {
  display: flex;
  flex-direction: column;
}

.cart {
  position: fixed;
  top: 1rem;
  right: 1rem;
  border: 1px solid grey;
  border-radius: 0.5rem;
  padding: 0.5rem;
  background-color: white;
}

.review_section {
  display: flex;
  margin-top: 2rem;
  column-gap: 5rem;
}

@media only screen and (max-width: 900px) {
  .review_section {
    flex-direction: column;
  }
}
</style>
