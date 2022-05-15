<script setup lang="ts">
import { ref, toRefs } from "vue";
interface Props {
  title: string;
  inventory: number;
  onSale: boolean;
  details: string[];
  variants: { color: string; image: string }[];
  sizes: string[];
  cart: number;
  addToCart: () => void;
}

const props = defineProps<Props>();

const { variants, sizes } = toRefs(props);

const color = ref(variants.value[0].color);
const size = ref(sizes.value[0]);

const updateColor = (newColor: string) => {
  color.value = newColor;
};

const updateSize = (newSize: string) => {
  size.value = newSize;
};
</script>

<template>
  <div class="card">
    <img
      class="product_image"
      :src="
        variants[variants.findIndex((variant) => variant.color === color)].image
      "
    />
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
          <div class="radio_button_group">
            <label
              v-for="variant in variants"
              :key="variant.color"
              class="radio_option"
            >
              <input
                type="radio"
                :id="variant.color"
                name="color"
                :value="variant.color"
                :defaultChecked="variant.color === color"
                @click="updateColor(variant.color)"
              />
              {{ variant.color }}
            </label>
          </div>
          <!-- <li v-for="variant in variants" :key="variant.color">
            {{ variant.color }}
          </li> -->
          <!-- </ul> -->
        </div>
        <div>
          <h2>Size</h2>
          <li v-for="size in sizes" :key="size">{{ size }}</li>
        </div>
      </div>
    </div>
    <button class="add_to_cart_button" @click="addToCart">Add to cart</button>
  </div>
</template>

<style>
@media only screen and (max-width: 900px) {
  .card {
    flex-direction: column;
  }

  h1 {
    margin-top: 1rem;
  }
}
.card {
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

.radio_button_group {
  display: flex;
  flex-direction: column;
}

.radio_option {
  cursor: pointer;
}
</style>
