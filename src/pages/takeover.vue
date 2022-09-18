<template>
  <div class="max-w-5xl mx-auto mt-60">
    <!-- <div class="originalContainer" ref="originalContainer">
      <div
        @click="moveBox"
        class="box w-20 h-20 bg-red-400 z-10 relative"
        ref="box"
      ></div>
    </div>
    <div
      class="bg-blue-400 w-64 h-64 -rotate-[15deg] ml-64 newContainer absolute top-32"
      ref="newContainer"
    ></div> -->
    <div class="grid grid-cols-4 gap-8">
      <Card v-for="card in cards" :key="card.id" v-bind="card" />
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
import { gsap } from "gsap";
import { Flip } from "gsap/Flip";
import Card from "../components/card.vue";
gsap.registerPlugin(Flip);
const originalContainer = ref();
const newContainer = ref();
const box = ref();
const moveBox = () => {
  const state = Flip.getState(box.value);
  console.log("state:", state);
  console.log(
    "box, og, new",
    box.value,
    originalContainer.value,
    newContainer.value
  );
  box.value.parentNode === originalContainer.value
    ? newContainer.value.appendChild(box.value)
    : originalContainer.value.appendChild(box.value);

  Flip.from(state, {
    duration: 1.2,
    ease: "power4.out",
  });
};
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
