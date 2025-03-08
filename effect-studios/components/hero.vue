<template>
  <div class="min-h-screen flex flex-col">
    <!-- Main Content -->
    <main
      class="flex-grow flex flex-col items-center justify-center py-12 px-4 bg-[#F8F9FE]"
    >
      <div
        class="container mx-auto w-full max-w-6xl h-1/2 flex items-center justify-center mb-8"
      >
        <!-- Phone Mockup desktop -->
        <div class="w-full md:w-1/2 justify-center hidden sm:flex">
          <div class="relative w-64 h-[500px]">
            <div
              class="absolute inset-0 bg-green-500 rounded-[40px] shadow-xl"
            ></div>
            <div class="absolute inset-[6px] bg-[#1e3a8a] rounded-[36px]"></div>
          </div>
        </div>

        <!-- Phone Mockup mobile -->
        <div class="w-full md:hidden flex justify-center lg:hidden">
          <div class="relative w-64 h-[500px]">
            <img
              src="/images/hero-mobile.png"
              alt="phone"
              class="object-contain"
            />
          </div>
        </div>
      </div>
      <!-- Slider Content small screen -->
      <div class="text-center max-w-md block lg:hidden">
        <h1 class="text-3xl font-extrabold text-[#0D2C65] leading-tight">
          Multi-currency accounts for Africans
        </h1>
        <p class="text-[#233375] text-sm mt-4">
          Transact at home and abroad - create, send, hold, receive money in
          African currencies and foreign currencies while also sending money to
          and from Africa seamlessly.
        </p>

        <!-- Play Button -->
        <div class="flex items-center justify-start mt-6">
          <button
            class="flex items-center space-x-2 bg-transparent text-[#233375] font-medium"
          >
            <div
              class="w-10 h-10 flex items-center justify-center rounded-full border border-[#233375] "
            >
              <svg
                class="w-4 h-4 text-[#233375]"
                viewBox="0 0 24 24"
                fill="bg-[#233375]"
                stroke="currentColor"
                stroke-width="2"
                stroke-linecap="round"
                stroke-linejoin="round"
              >
                <polygon points="5 3 19 12 5 21 5 3"></polygon>
              </svg>
            </div>
            <span>See how it works</span>
          </button>
        </div>

            <!-- arrow down Button -->
            <div class="flex items-center justify-start mt-6">
          <button
            class="flex items-center space-x-2 bg-transparent text-[#233375] font-medium"
          >
          
            <svg
              xmlns="http://www.w3.org/2000/svg"
              class="h-5 w-5 ml-1 text-green-500"
              fill="none"
              viewBox="0 0 24 24"
              stroke="currentColor"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M19 14l-7 7m0 0l-7-7m7 7V3"
              />
            </svg>
           
          </button>
        </div>
      </div>

      <!-- Slider Content large screen -->
      <div class="w-full max-w-none relative h-1/2">
        <transition-group
          :name="transitionName"
          tag="div"
          class="absolute w-full mb-16 sm:mb-96"
        >
          <div
            v-for="(slide, index) in slides"
            :key="index"
            v-show="currentSlide === index"
            class="transition-all duration-500 flex-col md:flex-row items-center justify-between w-full text-center md:text-left font-bold hidden sm:flex"
          >
            <!-- Title on the far left -->
            <h1
              class="text-6xl md:text-4xl text-[#0D2C65] mb-4 w-full md:w-1/2 text-left ml-8 font-extrabold"
            >
              {{ slide.title }}
            </h1>

            <!-- Description with highlighted words -->
            <p class="text-[#233375] mb-8 md:w-1/2 text-right mr-8 font-light">
              <template v-for="(part, idx) in slide.description" :key="idx">
                <span v-if="part.highlight" :class="part.color">{{
                  part.text
                }}</span>
                <span v-else>{{ part.text }}</span>
              </template>
            </p>
          </div>
        </transition-group>

        <!-- Slider Indicators -->
        <div class="space-x-2 lg:mt-16 sm:flex hidden w-full">
          <button
            v-for="(_, index) in slides"
            :key="index"
            @click="goToSlide(index)"
            class="h-0.5 transition-all duration-300 rounded-none flex-1 cursor-pointer"
            :class="[index <= currentSlide ? 'bg-blue-500' : 'bg-gray-300']"
          ></button>
        </div>

        <!-- Wrapper for News Items & Scroll Down -->
        <div
          class="mt-12 text-sm text-gray-600 w-full justify-between items-center sm:flex hidden"
        >
          <!-- News Items -->
          <div class="font-light">
            <div class="flex items-center mb-2 ml-8">
              <span class="text-gray-400 mr-2">News & Release update </span>
            </div>
            <div class="flex items-center mb-2 ml-8">
              <span class="text-gray-400 mr-2">June 20, 2023 —</span>
              <span class="text-blue-500"
                >Bomba now has a dollar wallet, activate your account</span
              >
            </div>
            <div class="flex items-center ml-8">
              <span class="text-gray-400 mr-2">June 01, 2022 —</span>
              <span class="text-blue-500"
                >Top 10 Summer Vacation Places in 2022</span
              >
            </div>
          </div>

          <!-- Scroll Down -->
          <div class="flex items-center text-gray-600">
            <span>Scroll Down</span>
            <svg
              xmlns="http://www.w3.org/2000/svg"
              class="h-5 w-5 ml-1 text-green-500"
              fill="none"
              viewBox="0 0 24 24"
              stroke="currentColor"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M19 14l-7 7m0 0l-7-7m7 7V3"
              />
            </svg>
          </div>
        </div>
      </div>
    </main>
  </div>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount, computed } from "vue";

// Slide data
const slides = [
  {
    title: "Multi-currency accounts for Africans",
    description: [
      {
        text: "Transact at home and abroad - create, send, hold and receive money in African and foreign currencies. Send money to and from Africa, seamlessly.s",
        highlight: false,
      },
    ],
  },
  {
    title: "Choose from several payment methods",
    description: [
      {
        text: "With Bomba, you get to choose how you send and receive money; ",
        highlight: false,
      },
      {
        text: "'Swap'",
        highlight: true,
        color: "text-green-600 font-semibold",
      },
      { text: ", ", highlight: false },
      {
        text: "'Express'",
        highlight: true,
        color: "text-green-500 font-semibold",
      },
      { text: ", or ", highlight: false },
      {
        text: "'Withdraw Money'",
        highlight: true,
        color: "text-green-500 font-semibold",
      },
      { text: ".", highlight: false },
    ],
  },
  {
    title: "Accept and create offers with Swap",
    description: [
      {
        text: "You can send money internationally at your preferred rate on our",
        highlight: false,
      },
      {
        text: "Peer-to-peer Marketplace",
        highlight: true,
        color: "text-green-500 font-semibold",
      },
      { text: " by choosing or accepting an offer.", highlight: false },
    ],
  },
  {
    title: "Make instant transfers with Express",
    description: [
      { text: "When you send money using ", highlight: false },
      {
        text: "'Express'",
        highlight: true,
        color: "text-green-500 font-semibold",
      },
      {
        text: " - it’s sent at Bomba exchange rate and your transaction is completed instantly.",
        highlight: false,
      },
    ],
  },
  {
    title: "Review and confirm your transaction",
    description: [
      {
        text: "Review your transaction, ensure that the provided details are correct, then click the send button!",
        highlight: false,
      },
    ],
  },
  {
    title: "Completed! Fast, easy and secure",
    description: [
      {
        text: "Money on its way! Send money today to your friends, family or make payment to a business.",
        highlight: false,
      },
    ],
  },
];

// State
const currentSlide = ref(0);
const direction = ref("right");
const timer = ref(null);
const slideInterval = 5000; // 5 seconds

// Computed properties
const transitionName = computed(() => "slide-fade"); // Always slide right

// Methods
const nextSlide = () => {
  direction.value = "right"; // Ensure rightward movement
  currentSlide.value = (currentSlide.value + 1) % slides.length;
};

const prevSlide = () => {
  nextSlide(); // Make "prev" function act like "next" to always go right
};

const goToSlide = (index) => {
  direction.value = "right"; // Always transition right
  currentSlide.value = index;
  resetTimer();
};

const resetTimer = () => {
  clearInterval(timer.value);
  startTimer();
};

const startTimer = () => {
  timer.value = setInterval(() => {
    nextSlide();
  }, slideInterval);
};

// Lifecycle hooks
onMounted(() => {
  startTimer();
});

onBeforeUnmount(() => {
  clearInterval(timer.value);
});
</script>

<style scoped>
/* Slide Out Left (Current Slide Leaving) */
.slide-right-leave-active {
  transition: transform 0.5s ease-in-out, opacity 0.5s;
}
.slide-right-leave-to {
  transform: translateX(-100%);
  opacity: 0;
}

/* Slide In from Right (New Slide Entering) */
.slide-right-enter-active {
  transition: transform 0.5s ease-in-out, opacity 0.5s;
}
.slide-right-enter-from {
  transform: translateX(100%);
  opacity: 0;
}

.slide-fade-enter-active {
  transition: all 0.8s ease-in-out;
}
.slide-fade-leave-active {
  transition: all 0.8s ease-in-out;
  opacity: 0;
}
.slide-fade-enter {
  transform: translateX(50px);
  opacity: 0;
}
.slide-fade-leave-to {
  transform: translateX(-50px);
  opacity: 0;
}
</style>
