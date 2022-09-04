<script setup>
import { ref, onMounted, reactive, nextTick } from "vue";
import confetti from "canvas-confetti";

const before = reactive([10000, 9500, 9000, 8500, 8000]);
const after = reactive([6000, 5500, 5000, 4500, 4000]);

const fullscreen = ref(false);

const container = ref();
const selected = ref();
const content = ref();

const anim = reactive({});

const tl = gsap.timeline();
onMounted(() => {
  const containerDiv = container.value;
  const selectedDiv = selected.value;
  tl.set(selectedDiv, {
    y: "-100vh",
    x: "110%",
    opacity: 0,
    height: 0,
    marginTop: 0,
    marginBottom: 0,
  });
  tl.fromTo(
    containerDiv,
    {
      y: "110vh",
    },
    {
      duration: 3,
      y: "-60vh",
      ease: "power3.inOut",
    }
  );
  tl.to(
    selectedDiv,
    {
      duration: 2,
      y: 0,
      opacity: 1,
      margin: "1.5rem 0",
      height: "10rem",
      ease: "power3.inOut",
    },
    "-=1"
  );
  tl.to(selectedDiv, {
    duration: 1.5,
    x: 0,
    ease: "elastic.out(2, 1)",
  });
  tl.to(selectedDiv, {
    scale: 1.1,
    yoyo: true,
    repeat: -1,
    ease: "power1.inOut",
  });
});

const takeOver = () => {
  const selectedDiv = selected.value;
  const contentDiv = content.value;
  const pos = selectedDiv.getBoundingClientRect();
  if (fullscreen.value) return;
  console.log("pos:", pos);
  tl.pause();
  gsap.set(selectedDiv, {
    clearProps: "transform",
    pointerEvents: "none",
  });
  gsap.set(contentDiv, {
    position: "fixed",
    pointerEvents: "none",
  });

  anim.value = gsap.to(contentDiv, {
    width: "100vw",
    height: "120vh",
    top: "50vh",
    paddingTop: "14rem",
    left: 0,
    duration: 2,

    ease: "power3.inOut",
    onComplete: () => {
      createConfetti();
      fullscreen.value = true;
      nextTick(() => {
        const tl = gsap.timeline();
        const playAgainText = document.querySelector("#playAgainText");
        const playAgainButton = document.querySelector("#playAgainButton");

        tl.from(playAgainText, {
          opacity: 0,
          y: 80,
          duration: 1.2,
          ease: "power3.inOut",
        });
        tl.from(
          playAgainButton,
          {
            opacity: 0,
            y: 80,
            duration: 1.2,
            ease: "power3.inOut",
          },
          "-=0.8"
        );
        tl.to(
          playAgainButton,
          {
            scale: 1.1,
            yoyo: true,
            repeat: -1,
            ease: "power1.inOut",
          },
          "-=0.8"
        );
      });
    },
  });
};

const exitFullscreen = () => {
  console.log("EXIT");
  const containerDiv = container.value;
  console.log("anim ", anim.value);

  const tl = gsap.timeline();
  console.log("playAgainText in exit", playAgainText);
  tl.to(playAgainText, {
    opacity: 0,
    y: -80,
    duration: 0.5,
    ease: "power3.inOut",
  });
  tl.to(
    playAgainButton,
    {
      opacity: 0,
      y: -80,
      duration: 0.5,
      ease: "power3.inOut",
      onComplete: () => {
        anim.value.timeScale(1.2).reverse();
        fullscreen.value = false;
      },
    },
    "-=0.25"
  );
  tl.to(containerDiv, {
    y: "-230vh",
    duration: 1.5,
    ease: "back.inOut(2)",
    delay: 1.6,
  });
};

const createConfetti = () => {
  var duration = 5 * 1000;
  var animationEnd = Date.now() + duration;
  var defaults = { startVelocity: 30, spread: 360, ticks: 60, zIndex: 0 };

  function randomInRange(min, max) {
    return Math.random() * (max - min) + min;
  }

  var interval = setInterval(function () {
    var timeLeft = animationEnd - Date.now();

    if (timeLeft <= 0) {
      return clearInterval(interval);
    }

    var particleCount = 50 * (timeLeft / duration);
    // since particles fall down, start a bit higher than random
    confetti(
      Object.assign({}, defaults, {
        particleCount,
        origin: { x: randomInRange(0.1, 0.3), y: Math.random() - 0.2 },
      })
    );
    confetti(
      Object.assign({}, defaults, {
        particleCount,
        origin: { x: randomInRange(0.7, 0.9), y: Math.random() - 0.2 },
      })
    );
  }, 250);
};
</script>

<template>
  <div
    class="w-screen h-screen bg-gray-800 text-white overflow-hidden relative"
  >
    <div ref="container" class="flex justify-center">
      <ul class="flex flex-col">
        <li v-for="i in before" :key="`before-${i}`" class="card">
          <p
            class="text-sm uppercase font-semibold text-gray-500 tracking-wider"
          >
            Highscore
          </p>
          <p class="text-7xl font-bold text-gray-900">{{ i }}</p>
        </li>
        <li
          @click="takeOver"
          ref="selected"
          class="card !bg-red-400 !p-0 flex items-center justify-center cursor-pointer"
        >
          <div ref="content" class="bg-red-400">
            <p
              class="text-8xl font-bold text-white text-center leading-none -mt-4"
            >
              7000
            </p>
            <div v-if="fullscreen">
              <p
                id="playAgainText"
                class="font-bold text-white text-center text-4xl mt-24"
              >
                Great job! You have taken over the world. Would you like to play
                again?
              </p>
              <button
                @click="exitFullscreen"
                id="playAgainButton"
                class="rounded-full bg-white w-28 h-28 block mx-auto mt-8 pointer-events-auto"
              >
                <!-- cross svg icon -->
                <svg
                  version="1.1"
                  id="Layer_1"
                  xmlns="http://www.w3.org/2000/svg"
                  xmlns:xlink="http://www.w3.org/1999/xlink"
                  x="0px"
                  y="0px"
                  viewBox="0 0 512 512"
                  style="enable-background: new 0 0 512 512"
                  xml:space="preserve"
                >
                  <circle style="fill: #1fcfc1" cx="256" cy="256" r="245.801" />
                  <polygon
                    style="fill: #f2f2f2"
                    points="195.825,391.629 376.351,256 195.825,120.371 "
                  />
                  <g>
                    <path
                      style="fill: #4d4d4d"
                      d="M256,512c-68.381,0-132.667-26.628-181.019-74.98C26.628,388.667,0,324.38,0,256
		S26.628,123.333,74.981,74.98C123.333,26.628,187.619,0,256,0s132.667,26.628,181.019,74.98C485.372,123.333,512,187.62,512,256
		s-26.628,132.667-74.981,181.02C388.667,485.372,324.381,512,256,512z M256,20.398C126.089,20.398,20.398,126.089,20.398,256
		S126.089,491.602,256,491.602S491.602,385.911,491.602,256S385.911,20.398,256,20.398z"
                    />
                    <path
                      style="fill: #4d4d4d"
                      d="M195.824,401.828c-1.553,0-3.115-0.355-4.557-1.075c-3.458-1.727-5.641-5.26-5.641-9.124V120.371
		c0-3.864,2.185-7.397,5.641-9.124c3.458-1.726,7.593-1.351,10.685,0.97l180.526,135.629c2.564,1.927,4.073,4.948,4.073,8.154
		s-1.508,6.228-4.073,8.154L201.951,399.783C200.15,401.137,197.994,401.828,195.824,401.828z M206.024,140.791v230.418L359.371,256
		L206.024,140.791z"
                    />
                    <path
                      style="fill: #4d4d4d"
                      d="M256,473.243c-5.632,0-10.199-4.566-10.199-10.199c0-5.633,4.567-10.199,10.199-10.199
		c52.815,0,102.404-20.633,139.633-58.1c3.973-3.996,10.429-4.015,14.425-0.045c3.995,3.971,4.016,10.428,0.046,14.424
		C369.016,450.471,314.287,473.243,256,473.243z"
                    />
                    <path
                      style="fill: #4d4d4d"
                      d="M430.396,377.825c-1.886,0-3.793-0.522-5.498-1.617c-4.741-3.041-6.118-9.351-3.076-14.092
		c1.514-2.36,2.998-4.788,4.411-7.216c2.834-4.867,9.077-6.516,13.945-3.684c4.868,2.833,6.518,9.077,3.684,13.945
		c-1.56,2.681-3.201,5.363-4.873,7.97C437.043,376.168,433.754,377.825,430.396,377.825z"
                    />
                  </g>
                </svg>
              </button>
            </div>
          </div>
        </li>
        <li v-for="i in after" :key="`after-${i}`" class="card">
          <p
            class="text-sm uppercase font-semibold text-gray-500 tracking-wider"
          >
            Highscore
          </p>
          <p class="text-7xl font-bold text-gray-900">{{ i }}</p>
        </li>
      </ul>
    </div>
  </div>
</template>
