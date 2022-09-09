<template>
  <div
    class="py-4 pb-0 border-b border-gray-400 relative wrapper overflow-x-auto"
    ref="wrapper"
  >
    <ul class="flex space-x-4 whitespace-nowrap px-4">
      <li
        ref="tabRefs"
        v-for="tab in tabs"
        @click="onClick(tab.id, $event)"
        :key="tab.id"
        class="pb-5"
      >
        {{ tab.name }}
      </li>
    </ul>
    <div
      class="h-1 absolute left-0 bottom-0 highlight bg-red-500"
      :style="hlStyle"
    ></div>
  </div>

  <div class="relative p-8">
    <TransitionGroup name="list">
      <div
        v-for="tab in tabs"
        :key="tab.content"
        v-show="tab.id === selectedIndex"
      >
        {{ tab.content }}
      </div>
    </TransitionGroup>
  </div>
</template>

<script setup>
import { onMounted, ref } from "vue";

const selectedIndex = ref(0);
const wrapper = ref();

const tabs = ref([
  {
    name: "Test tab 1",
    id: 0,
    content:
      "Lorem ipsum dolor sit amet consectetur adipisicing elit. Possimus vero dolo",
  },
  {
    name: "Test tab 2 asasas",
    id: 1,
    content:
      "Another lorem here Lorem ipsum dolor, sit amet consectetur adipisicing elit. Soluta consectetur nobis veniam qui neque minus iste et beatae eius ex.",
  },
  {
    name: "Test tab 3 as asas",
    id: 2,
    content: "test.",
  },
  {
    name: "Test tab 3 as asas",
    id: 3,
    content: "test.",
  },
  {
    name: "Test tab 3 as asas",
    id: 4,
    content: "test.",
  },
  {
    name: "Test tab 3 as asas",
    id: 5,
    content: "test.",
  },
  {
    name: "Test tab 3 as asas",
    id: 6,
    content: "test.",
  },
]);

const hlStyle = ref(null);

const tabRefs = ref([]);

onMounted(() => {
  const firstRef = tabRefs.value[0];
  setTimeout(() => {
    updateHighlight(firstRef);
  }, 50);
});

const onClick = (index, { target }) => {
  selectedIndex.value = index;
  updateHighlight(target);
};

const updateHighlight = (node) => {
  const { left: wrapperLeft } = wrapper.value.getBoundingClientRect();
  console.log("wrapperLeft:", wrapperLeft);
  const { left: targetLeft } = node.getBoundingClientRect();
  const scrollLeft = wrapper.value.scrollLeft;
  const x = targetLeft - wrapperLeft + scrollLeft;
  console.log("targetLeft:", targetLeft);
  console.log("scrollLeft:", scrollLeft);
  console.log("x:", x);
  hlStyle.value = {
    transform: `translateX(${x}px) scale(1.1)`,
    width: `${node.offsetWidth}px`,
  };
};
</script>

<style scoped>
.highlight {
  transition: all 0.4s cubic-bezier(0.19, 0.02, 0.34, 1.14);
}

.flex-wrapper::-webkit-scrollbar {
  display: "none";
}

.list-enter-active,
.list-leave-active {
  position: absolute;
  transition: all 0.5s ease;
}

.list-enter-from {
  opacity: 0;
  transform: translateX(-100px);
}
.list-leave-to {
  opacity: 0;
  transform: translateX(100px);
}
</style>
