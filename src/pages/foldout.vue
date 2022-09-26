<template>
  <div>
    <div
      class="w-[300px] h-[440px] overflow-hidden"
      ref="imgCard"
      @click="toggleDescription"
      @mouseenter="showDescription"
      @mouseleave="hideDescription"
    >
      <div class="relative">
        <img
          class="object-cover aspect-square"
          src="https://images.unsplash.com/photo-1614113036347-9f60df80730a?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1497&q=80"
          alt=""
        />
      </div>

      <div class="relative" ref="description">
        <div class="w-full h-12 flex items-end absolute -top-11">
          <div class="w-1/4 h-[70%] bg-pink-300"></div>
          <div class="w-1/4 h-[30%] bg-pink-300"></div>
          <div class="w-1/4 h-[50%] bg-pink-300"></div>
          <div class="w-1/4 h-[80%] bg-pink-300"></div>
        </div>
        <div class="p-4 bg-pink-300">
          <h3 class="text-2xl font-bold">Here is the title for the card</h3>
          <div class="mt-4">
            <div class="flex justify-between items-center">
              <p>Mexico City, Mexico</p>
              <div
                class="w-8 h-8 rounded-full bg-white flex justify-center items-center"
              >
                <svg
                  class="stroke-current text-black w-4 h-4"
                  viewBox="0 0 10 10"
                  fill="none"
                  xmlns="http://www.w3.org/2000/svg"
                >
                  <g>
                    <path
                      id="vertical"
                      d="M5 1V9"
                      stroke-width="1.5"
                      stroke-linecap="round"
                      stroke-linejoin="round"
                    />
                    <path
                      d="M1 5H9"
                      stroke-width="1.5"
                      stroke-linecap="round"
                      stroke-linejoin="round"
                    />
                  </g>
                </svg>
              </div>
            </div>
            <p class="content">
              Lorem ipsum dolor sit amet consectetur, adipisicing elit.
              Accusantium aliquid praesentium deserunt assumenda blanditiis,
              maiores voluptas quos, quam odio, est voluptatum pariatur?
              Corporis sapiente nisi odio impedit consectetur mollitia eum,
              commodi laudantium asperiores voluptatem veritatis voluptas quod
              suscipit, ipsum odit molestiae dolorem eos quibusdam reiciendis.
              Earum ratione rerum qui dolore! dolorem eos quibusdam reiciendis.
              Earum ratione rerum qui dolore! mollitia eum, commodi laudantium
              asperiores voluptatem veritatis voluptas quod suscipit, ipsum odit
              molestiae dolorem eos quibusdam reiciendis. Earum ratione rerum
              qui dolore! dolorem eos quibusdam reiciendis. Earum ratione rerum
              qui dolore!
            </p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { onMounted, ref } from "vue";
import { MorphSVGPlugin } from "../../vendor/MorphSVGPlugin";
const imgCard = ref();
const description = ref();
gsap.registerPlugin(MorphSVGPlugin);

const open = ref(false);

const tl = gsap.timeline({ paused: true });
onMounted(() => {
  console.log("MorphSVGPlugin:", MorphSVGPlugin);

  console.log("imgCard:", description);
  tl.to(description.value, {
    duration: 1,
    y: -300,
    ease: "power2.inOut",
  });

  tl.from(
    ".content",
    {
      duration: 1,
      opacity: 0,
      y: 40,
      ease: "power2.inOut",
    },
    "<"
  );
  tl.to(
    "#vertical",
    {
      // opacity: 0,
      duration: 1,
      transformOrigin: "center",
      rotate: "90deg",
      ease: "power2.inOut",
    },
    "<"
  );
});

const showDescription = () => {
  tl.play();
};
const hideDescription = () => {
  tl.reverse();
};
const toggleDescription = () => {
  if (!open.value) {
    showDescription();
  } else {
    hideDescription();
  }
  open.value = !open.value;
};
</script>

<style lang="scss" scoped></style>
