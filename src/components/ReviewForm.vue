<script setup lang="ts">
import { ref, toRefs } from "vue";
import type { IReview } from "@/types";

interface Props {
  onSubmit: ({ name, review, rating }: IReview) => void;
}

const props = defineProps<Props>();
const { onSubmit } = toRefs(props);

// Review form values
const name = ref("");
const review = ref("");
const rating = ref(5);
const submitForm = () => {
  onSubmit.value({
    name: name.value,
    review: review.value,
    rating: rating.value,
  });
  name.value = "";
  review.value = "";
  rating.value = 5;
};
</script>

<template>
  <form class="review_form" @submit.prevent="submitForm">
    <h2>Leave a review</h2>
    <label>Name: <input v-model="name" /></label>

    <label class="label">Review: <textarea v-model="review"></textarea></label>

    <label
      >Rating:
      <select v-model.number="rating" class="select">
        <option>5</option>
        <option>4</option>
        <option>3</option>
        <option>2</option>
        <option>1</option>
      </select></label
    >

    <input class="button" type="submit" value="Submit" />
  </form>
</template>

<style scoped>
.review_form {
  display: flex;
  flex-direction: column;
  padding: 3rem;
  box-shadow: rgba(0, 0, 0, 0.24) 0px 3px 8px;
  width: fit-content;
  border-radius: 1rem;
  height: fit-content;
}

.button {
  padding: 0.5rem;
  width: fit-content;
  background-color: black;
  color: white;
  border: none;
  border-radius: 1rem;
  font-weight: bold;
  cursor: pointer;
  margin-top: 1rem;
}

label {
  display: flex;
  margin: 0.5rem 0;
  column-gap: 0.5rem;
}

.select {
  position: relative;
  top: 2px;
}

@media only screen and (max-width: 900px) {
  .review_form {
    width: 335px;
  }
}
</style>
