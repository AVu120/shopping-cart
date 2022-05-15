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
  removeFromCart: () => void;
}

const props = defineProps<Props>();

const { variants, sizes, inventory } = toRefs(props);

const color = ref(variants.value[0].color);
const size = ref(sizes.value[0]);
const hoverColor = ref(variants.value[0].color);

const updateColor = (newColor: string) => {
  color.value = newColor;
};
const updateHoverColor = (newColor: string) => {
  hoverColor.value = newColor;
};

const updateSize = (newSize: string) => {
  size.value = newSize;
};

const isOutOfStock = inventory.value === 0;
</script>

<template>
  <div class="card">
    <div class="contents">
      <img
        class="product_image"
        :class="{ out_of_stock_product: isOutOfStock }"
        :src="
          variants[
            variants.findIndex((variant) => variant.color === hoverColor)
          ]?.image ||
          variants[variants.findIndex((variant) => variant.color === color)]
            .image
        "
      />
      <div class="product_info">
        <h1>{{ title + (onSale ? " - On Sale" : "") }}</h1>
        <div v-if="inventory > 0" class="product_in_stock">
          <p v-if="inventory > 10">In Stock</p>
          <p v-else-if="inventory > 0">Almost sold out!</p>
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
                @mouseover="updateHoverColor(variant.color)"
                @mouseleave="updateHoverColor('')"
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
    </div>
    <div class="cart_button_group">
      <p v-if="isOutOfStock">Out of stock</p>
      <button
        v-if="inventory > 0"
        class="add_to_cart_button"
        @click="addToCart"
        :style="{ cursor: isOutOfStock ? 'not-allowed' : 'pointer' }"
      >
        Add to cart
      </button>
      <button
        v-if="cart > 0"
        class="add_to_cart_button"
        @click="removeFromCart"
      >
        Remove from cart
      </button>
    </div>
  </div>
</template>

<style scoped>
.card {
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: lightblue;
  padding: 2rem;
  border-radius: 2rem;
  width: fit-content;
}

.contents {
  display: flex;
  align-items: center;
  justify-content: center;
}
.product_image {
  height: 300px;
  width: 300px;
  border: 1px solid grey;
  border-radius: 1rem;
  margin-right: 2rem;
}

.out_of_stock_product {
  opacity: 0.5;
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

.cart_button_group {
  display: flex;
  column-gap: 1rem;
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
  margin-top: 1rem;
}

.radio_button_group {
  display: flex;
  flex-direction: column;
}

.radio_option {
  cursor: pointer;
}
@media only screen and (max-width: 900px) {
  .contents {
    flex-direction: column;
  }

  h1 {
    margin-top: 1rem;
  }

  .product_image {
    height: 200px;
    width: 200px;
  }
}
</style>
