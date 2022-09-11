<script setup>
import { ref, onMounted } from "vue";
const glassCard = ref();
onMounted(() => {
  const tl = gsap.timeline();

  tl.from(glassCard.value, {
    delay: 0.4,
    duration: 1.2,
    opacity: 0,

    height: 0,
    ease: "power3.inOut",
  });
  tl.from(
    ".fade-in",
    {
      duration: 1,
      opacity: 0,
      y: 20,
      stagger: {
        each: 0.2,
      },
      ease: "power3.inOut",
    },
    "-=0.5"
  );
});
</script>
<template>
  <div
    class="w-screen h-screen flex justify-center items-center overflow-hidden"
  >
    <div
      class="w-screen h-screen bg-[url('/triangle-pattern.png')] background absolute"
    ></div>
    <div
      ref="glassCard"
      class="glass-card w-[460px] p-8 text-center shadow-2xl"
    >
      <img
        class="rounded-full w-32 h-32 object-cover mx-auto mb-8 shadow-xl fade-in"
        src="https://images.unsplash.com/photo-1580489944761-15a19d654956?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=761&q=80"
        alt=""
      />
      <p class="font-bold text-3xl text-gray-800 fade-in">Mads Brodt</p>
      <p class="mt-4 text-gray-700 fade-in">Front-end Developer</p>

      <div class="mt-8 flex gap-8 justify-center fade-in">
        <div>
          <p class="font-bold text-2xl text-gray-700">100</p>
          <p
            class="text-gray-600 text-xs mt-2 font-semibold tracking-widest uppercase"
          >
            Followers
          </p>
        </div>
        <div>
          <p class="font-bold text-2xl text-gray-700">50</p>
          <p
            class="text-gray-600 text-xs mt-2 font-semibold tracking-widest uppercase"
          >
            References
          </p>
        </div>
        <div>
          <p class="font-bold text-2xl text-gray-700">105</p>
          <p
            class="text-gray-600 text-xs mt-2 font-semibold tracking-widest uppercase"
          >
            projects
          </p>
        </div>
      </div>
      <div class="mt-8 flex gap-5 justify-center fade-in" id="some-icons">
        <button
          class="rounded-xl w-10 h-10 bg-gradient-to-tr from-blue-800 to-blue-600 flex justify-center items-center"
        >
          <svg class="w-4 h-4 text-white" viewBox="0 0 20 20">
            <path
              fill="currentColor"
              d="M17 1H3c-1.1 0-2 .9-2 2v14c0 1.101.9 2 2 2h7v-7H8V9.525h2v-2.05c0-2.164 1.212-3.684 3.766-3.684l1.803.002v2.605h-1.197c-.994 0-1.372.746-1.372 1.438v1.69h2.568L15 12h-2v7h4c1.1 0 2-.899 2-2V3c0-1.1-.9-2-2-2z"
            />
          </svg>
        </button>
        <button
          class="rounded-xl w-10 h-10 bg-gradient-to-tr from-sky-400 to-sky-600 flex justify-center items-center"
        >
          <svg class="w-4 h-4 text-white" viewBox="0 0 20 20">
            <path
              fill="currentColor"
              d="M17.316 6.246c.008.162.011.326.011.488c0 4.99-3.797 10.742-10.74 10.742c-2.133 0-4.116-.625-5.787-1.697a7.577 7.577 0 0 0 5.588-1.562a3.779 3.779 0 0 1-3.526-2.621a3.858 3.858 0 0 0 1.705-.065a3.779 3.779 0 0 1-3.028-3.703v-.047a3.766 3.766 0 0 0 1.71.473a3.775 3.775 0 0 1-1.168-5.041a10.716 10.716 0 0 0 7.781 3.945a3.813 3.813 0 0 1-.097-.861a3.773 3.773 0 0 1 3.774-3.773a3.77 3.77 0 0 1 2.756 1.191a7.602 7.602 0 0 0 2.397-.916a3.789 3.789 0 0 1-1.66 2.088a7.55 7.55 0 0 0 2.168-.594a7.623 7.623 0 0 1-1.884 1.953z"
            />
          </svg>
        </button>
        <button
          class="rounded-xl w-10 h-10 bg-gradient-to-tr from-purple-800 to-rose-500 flex justify-center items-center"
        >
          <svg class="w-4 h-4 text-white" viewBox="0 0 20 20">
            <path
              fill="currentColor"
              d="M17 1H3c-1.1 0-2 .9-2 2v14c0 1.101.9 2 2 2h14c1.1 0 2-.899 2-2V3c0-1.1-.9-2-2-2zM9.984 15.523a5.539 5.539 0 0 0 5.538-5.539c0-.338-.043-.664-.103-.984H17v7.216a.69.69 0 0 1-.693.69H3.693a.69.69 0 0 1-.693-.69V9h1.549c-.061.32-.104.646-.104.984a5.54 5.54 0 0 0 5.539 5.539zM6.523 9.984a3.461 3.461 0 1 1 6.922 0a3.461 3.461 0 0 1-6.922 0zM16.307 6h-1.615A.694.694 0 0 1 14 5.308V3.691c0-.382.31-.691.691-.691h1.615c.384 0 .694.309.694.691v1.616c0 .381-.31.693-.693.693z"
            />
          </svg>
        </button>
        <button
          class="rounded-xl w-10 h-10 bg-gradient-to-tr from-blue-600 to-blue-900 flex justify-center items-center"
        >
          <svg class="w-4 h-4 text-white" viewBox="0 0 20 20">
            <path
              fill="currentColor"
              d="M8.072 9.301s1.892-.147 1.892-2.459c0-2.315-1.548-3.441-3.51-3.441H0v12.926h6.454s3.941.129 3.941-3.816c-.001-.001.171-3.21-2.323-3.21zM2.844 5.697h3.61s.878 0 .878 1.344c0 1.346-.516 1.541-1.102 1.541H2.844V5.697zm3.427 8.332H2.844v-3.455h3.61s1.308-.018 1.308 1.775c0 1.512-.977 1.669-1.491 1.68zm9.378-7.341c-4.771 0-4.767 4.967-4.767 4.967s-.326 4.941 4.767 4.941c0 0 4.243.254 4.243-3.437H17.71s.072 1.391-1.988 1.391c0 0-2.184.152-2.184-2.25h6.423c.001-.001.709-5.612-4.312-5.612zm1.941 3.886h-4.074s.266-1.992 2.182-1.992s1.892 1.992 1.892 1.992zm.507-6.414H12.98v1.594h5.117V4.16z"
            />
          </svg>
        </button>
        <button
          class="rounded-xl w-10 h-10 bg-gradient-to-tr from-gray-800 to-gray-600 flex justify-center items-center"
        >
          <svg class="w-4 h-4 text-white" viewBox="0 0 20 20">
            <path
              fill="currentColor"
              d="M13.18 11.309c-.718 0-1.3.807-1.3 1.799c0 .994.582 1.801 1.3 1.801s1.3-.807 1.3-1.801c-.001-.992-.582-1.799-1.3-1.799zm4.526-4.683c.149-.365.155-2.439-.635-4.426c0 0-1.811.199-4.551 2.08c-.575-.16-1.548-.238-2.519-.238c-.973 0-1.945.078-2.52.238C4.74 2.399 2.929 2.2 2.929 2.2c-.789 1.987-.781 4.061-.634 4.426C1.367 7.634.8 8.845.8 10.497c0 7.186 5.963 7.301 7.467 7.301l1.734.002l1.732-.002c1.506 0 7.467-.115 7.467-7.301c0-1.652-.566-2.863-1.494-3.871zm-7.678 10.289h-.056c-3.771 0-6.709-.449-6.709-4.115c0-.879.31-1.693 1.047-2.369C5.537 9.304 7.615 9.9 9.972 9.9h.056c2.357 0 4.436-.596 5.664.531c.735.676 1.045 1.49 1.045 2.369c0 3.666-2.937 4.115-6.709 4.115zm-3.207-5.606c-.718 0-1.3.807-1.3 1.799c0 .994.582 1.801 1.3 1.801c.719 0 1.301-.807 1.301-1.801c0-.992-.582-1.799-1.301-1.799z"
            />
          </svg>
        </button>
      </div>
      <div class="mt-8 flex gap-4 justify-between">
        <div class="fade-in w-full">
          <button
            class="rounded-full bg-gradient-to-r from-blue-500 to-blue-700 text-white px-4 py-2 w-full hover:shadow-xl transition-all hover:-translate-y-1 duration-300 hover:shadow-blue-500"
          >
            Send message
          </button>
        </div>
        <div class="fade-in w-full">
          <button
            class="rounded-full bg-gradient-to-r from-pink-500 to-orange-500 text-white px-4 py-2 w-full hover:shadow-xl transition-all hover:-translate-y-1 duration-300 hover:shadow-orange-500"
          >
            Follow me
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Nunito:wght@600;700&display=swap");

.glass-card {
  font-family: "Nunito", sans-serif;

  backdrop-filter: blur(6px) saturate(149%);
  -webkit-backdrop-filter: blur(6px) saturate(149%);
  background-color: rgba(255, 255, 255, 0.3);
  border-radius: 12px;
  border: 1px solid rgba(209, 213, 219, 0.3);
}
</style>
