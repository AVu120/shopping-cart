<script setup lang="ts">
interface Props {
  reviews: { name: string; review: string; rating: number | null }[];
}

defineProps<Props>();
</script>

<template>
  <div class="container">
    <h2>Reviews:</h2>
    <div
      v-for="{ name, review, rating } in reviews"
      :key="review"
      class="review"
    >
      <li class="review_name">
        {{
          name +
          (rating //@ts-ignore
            ? " - " +
              Array.from({ length: rating })
                .map((_) => "&#9733;")
                .join("")
            : "")
        }}
      </li>
      <li class="review_text">{{ review }}</li>
    </div>
  </div>
</template>

<style scoped>
.container {
  box-shadow: rgba(0, 0, 0, 0.24) 0px 3px 8px;
  width: 100%;
  border-radius: 1rem;
  padding: 1rem 3rem;
}

.review {
}
.review_name {
  font-weight: bold;
}
.review_text {
  font-style: italic;
  list-style: none;
  padding-left: 1.5rem;
  overflow-wrap: break-word;
  line-height: 1rem;
}

@media only screen and (max-width: 900px) {
  .container {
    margin-top: 1rem;
    /* width: 335px; */
  }

  /* .review_text {
    inline-size: 335px;
  } */
}
</style>
