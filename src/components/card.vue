<template>
  <div class="w-full test-card relative" ref="card">
    <img
      class="opacity-0 absolute -left-24 test-img translate-y-24"
      src="https://prodaaudxpcms001st.blob.core.windows.net/cache/e/c/9/4/e/9/ec94e95a09dc85e0e50ed0b17f08bf54f469b938.webp"
      alt=""
    />
    <button
      @click="takeOver"
      :key="id"
      class="relative text-left bg-gray-200 p-4 h-full"
    >
      <div class="h-full flex flex-col" ref="content">
        <div class="flex-1">
          <p class="text-lg font-semibold">{{ title }}</p>
          <p class="mt-2 line-clamp-3 description">
            Lorem, ipsum dolor sit amet consectetur adipisicing elit. Sint
            similique provident laboriosam aut autem perferendis quo molestiae,
            dolorem commodi totam temporibus corporis eum amet ut rerum ratione
            pariatur vero quasi ipsam minima tempore ex quas vel possimus? Hic
            quisquam, iure quasi est culpa, aspernatur vel aperiam omnis tempore
            reprehenderit ipsam.
          </p>
        </div>
        <span class="text-gray-700 uppercase text-sm font-bold mt-8">{{
          label
        }}</span>
      </div>
    </button>
  </div>
</template>

<script setup>
import { defineProps, ref } from "vue";
import { Flip } from "gsap/Flip";
import { gsap } from "gsap";
defineProps({
  id: Number,
  title: String,
  description: String,
  label: String,
});

const card = ref();
const content = ref();

const takeOver = () => {
  const targets = document.querySelectorAll(".test-card");
  const state = Flip.getState(targets);
  targets.forEach((target) => {
    const targetImg = target.querySelector(".test-img"),
      targetDescription = target.querySelector(".description");
    targetDescription.classList.add("line-clamp-3");
    gsap.set(targetImg, {
      y: "6rem",
      opacity: 0,
    });
    target.classList.remove("open");
  });
  card.value.classList.toggle("open");
  card.value.querySelector(".description").classList.remove("line-clamp-3");
  const img = card.value.querySelector(".test-img");
  const tl = Flip.from(state, {
    absolute: true,
  });
  tl.to(
    img,

    {
      y: "-90%",
      duration: 1,
      ease: "power3.inOut",
      opacity: 1,
    }
  );
};
</script>

<style>
.open {
  grid-column: span 2;
  grid-row: span 2;
  z-index: 30;
}
</style>
