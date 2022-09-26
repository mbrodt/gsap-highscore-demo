<template>
  <div class="max-w-5xl mx-auto mt-60">
    <div class="grid grid-cols-4 gap-8">
      <Card v-for="card in cards" :key="card.id" v-bind="card" />
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

const cards = ref([
  {
    id: 1,
    title: "First card",
    description:
      "Lorem ipsum dolor sit amet, consectetur adipiscing elit. consectetur adipiscing elit.",
    label: "Aalborg",
  },
  {
    id: 2,
    title: "Second card",
    description:
      "Lorem ipsum dolor sit amet, consectetur adipiscing elit. consectetur adipiscing elit.",
    label: "Aalborg",
  },
  {
    id: 3,
    title: "Third card",
    description:
      "Lorem ipsum dolor sit amet, consectetur adipiscing elit. consectetur adipiscing elit.",
    label: "Aalborg",
  },
  {
    id: 4,
    title: "Fourth card",
    description:
      "Lorem ipsum dolor sit amet, consectetur adipiscing elit. consectetur adipiscing elit.",
    label: "Aalborg",
  },
  {
    id: 5,
    title: "Fifth card",
    description:
      "Lorem ipsum dolor sit amet, consectetur adipiscing elit. consectetur adipiscing elit.",
    label: "Aalborg",
  },
  {
    id: 6,
    title: "Sixth card",
    description:
      "Lorem ipsum dolor sit amet, consectetur adipiscing elit. consectetur adipiscing elit.",
    label: "Aalborg",
  },
  {
    id: 7,
    title: "Seventh card",
    description:
      "Lorem ipsum dolor sit amet, consectetur adipiscing elit. consectetur adipiscing elit.",
    label: "Aalborg",
  },
  {
    id: 8,
    title: "Eigth card",
    description:
      "Lorem ipsum dolor sit amet, consectetur adipiscing elit. consectetur adipiscing elit.",
    label: "Aalborg",
  },
  {
    id: 9,
    title: "Ninth card",
    description:
      "Lorem ipsum dolor sit amet, consectetur adipiscing elit. consectetur adipiscing elit.",
    label: "Aalborg",
  },
  {
    id: 10,
    title: "Tenth card",
    description:
      "Lorem ipsum dolor sit amet, consectetur adipiscing elit. consectetur adipiscing elit.",
    label: "Aalborg",
  },
  {
    id: 11,
    title: "Eleventh card",
    description:
      "Lorem ipsum dolor sit amet, consectetur adipiscing elit. consectetur adipiscing elit. Lorem ipsum dolor sit amet, consectetur adipiscing elit. consectetur adipiscing elit.",
    label: "Aalborg",
  },
  {
    id: 12,
    title: "Twelvth card",
    description:
      "Lorem ipsum dolor sit amet, consectetur adipiscing elit. consectetur adipiscing elit.",
    label: "Aalborg",
  },
]);
</script>

<style>
.test-card:nth-child(odd) {
  background-color: #f1f5f9;
}
.test-card:nth-child(even) {
  background-color: #f5f5f5;
}
</style>
