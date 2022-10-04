<!-- <script setup>
import { ref, computed } from "vue";

import { usePointerSwipe } from "@vueuse/core";
const target = ref(null);
const container = ref(null);

const containerWidth = computed(() => container.value?.offsetWidth);
const left = ref("0");
const opacity = ref(1);

const { isSwiping, distanceX } = usePointerSwipe(target, {
  onSwipe(e) {
    console.log("distanceX:", distanceX.value);
    if (containerWidth.value) {
      if (distanceX.value < 0) {
        const distance = Math.abs(distanceX.value);
        left.value = `${distance}px`;
      } else {
        left.value = "0";
      }
    }
  },
  onSwipeEnd(e, direction) {
    console.log("e:", e);
    if (
      distanceX.value < 0 &&
      containerWidth.value &&
      Math.abs(distanceX.value) / containerWidth.value >= 0.5
    ) {
      left.value = `${containerWidth.value - target.value.clientWidth}px`;
    } else {
      left.value = "0";
    }
  },
});
</script>

<template>
  <div
    ref="container"
    class="w-[300px] h-[100px] bg-green-400 flex items-center rounded-full"
  >
    <div
      ref="target"
      class="ml-4 w-16 h-16 rounded-full bg-blue-400"
      :style="{ transform: `translateX(${left})` }"
    ></div>
  </div>
  {{ isSwiping }}
  {{ left }}
  {{ opacity }}
</template> -->

<script setup>
import { ref, computed, onMounted } from "vue";
import gsap from "gsap";
import { InertiaPlugin } from "../../vendor/InertiaPlugin";
import { Draggable } from "gsap/Draggable";
gsap.registerPlugin(Draggable);
gsap.registerPlugin(InertiaPlugin);

const target = ref(null);
const container = ref(null);
const background = ref(null);

const tl = gsap.timeline({ paused: true });

onMounted(() => {
  tl.fromTo(
    background.value,
    {
      scaleX: 0,
    },
    {
      ease: "linear",
      scaleX: 1,
    }
  );
  const updateProgress = (x) => {
    const pct = x / (container.value.offsetWidth - target.value.offsetWidth);

    console.log("pct:", pct);
    tl.progress(pct);
  };
  Draggable.create(target.value, {
    type: "x",
    bounds: container.value,
    inertia: true,
    minDuration: 0.5,
    maxDuration: 1,
    overshootTolerance: 0,
    onThrowUpdate() {
      updateProgress(this.x);
    },
    onDrag() {
      updateProgress(this.x);
    },
    snap: {
      x: function (endValue) {
        const containerWidth = container.value?.offsetWidth;

        if (endValue < containerWidth * 0.6) {
          return 0;
        } else {
          console.log("do end move");
          return containerWidth;
        }
      },
    },
  });
});
</script>

<template>
  <div
    ref="container"
    class="w-[500px] h-[100px] bg-green-400 flex items-center rounded-full relative overflow-hidden"
  >
    <div
      ref="target"
      class="h-24 aspect-square rounded-full bg-blue-400 relative"
    ></div>
    <div
      ref="background"
      class="w-full h-full bg-blue-600 absolute top-0 origin-left"
    ></div>
    <p
      class="text-white absolute top-1/2 -translate-y-1/2 left-1/2 top-0 -translate-x-1/2 font-semibold uppercase tracking-wide text-lg"
    >
      I'm done building
    </p>
  </div>
</template>
