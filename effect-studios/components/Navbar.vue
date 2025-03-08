<template>
  <nav class="border-b py-4 px-6 bg-white shadow-md">
    <div class="container mx-auto flex items-center justify-center">
      <!-- Left: Logo (If Any) -->
      <div></div>

      <!-- Desktop Navigation -->
      <div class="hidden md:flex items-center justify-center space-x-6">
        <div class="relative group">
          <a
            href="#"
            class="text-gray-600 hover:text-gray-900 flex items-center"
          >
            Features
            <svg
              xmlns="http://www.w3.org/2000/svg"
              class="h-4 w-4 ml-1"
              fill="none"
              viewBox="0 0 24 24"
              stroke="currentColor"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M19 9l-7 7-7-7"
              />
            </svg>
          </a>
        </div>
        <a href="#" class="text-gray-600 hover:text-gray-900">Help</a>
        <div class="relative group">
          <a
            href="#"
            class="text-gray-600 hover:text-gray-900 flex items-center"
          >
            Company
            <svg
              xmlns="http://www.w3.org/2000/svg"
              class="h-4 w-4 ml-1"
              fill="none"
              viewBox="0 0 24 24"
              stroke="currentColor"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M19 9l-7 7-7-7"
              />
            </svg>
          </a>
        </div>
        <a href="/press" class="text-gray-600 hover:text-gray-900">Press</a>

      </div>


    </div>

    <div class="container flex mx-auto items-center justify-end">
      <div></div>
      <!-- Mobile Menu Button -->
      <button
        @click="toggleMenu"
        class="md:hidden text-gray-600 hover:text-gray-900 focus:outline-none"
      >
        <svg
          xmlns="http://www.w3.org/2000/svg"
          class="h-6 w-6"
          fill="none"
          viewBox="0 0 24 24"
          stroke="currentColor"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M4 6h16M4 12h16m-7 6h7"
          />
        </svg>
      </button>
    </div>



    <!-- Mobile Menu  -->
    <div
      v-if="isOpen"
      class="md:hidden bg-[#1e3a8a] text-white shadow-lg fixed mt-6 w-full z-50 flex flex-col items-center justify-center space-y-6"
    >
      <a href="#" class="text-lg hover:text-gray-300">Features</a>
      <a href="#" class="text-lg hover:text-gray-300">Help</a>
      <a href="#" class="text-lg hover:text-gray-300">Company</a>
      <a href="/press" class="text-gray-600 hover:text-gray-900">Press</a>


      <!-- Close Button -->
      <button @click="toggleMenu" class="mt-6 text-gray-300 hover:text-white">
        Close Menu ✖
      </button>
    </div>
  </nav>
</template>

<script setup>
import { ref } from "vue";

const isOpen = ref(false);
const toggleMenu = () => {
  isOpen.value = !isOpen.value;
};
</script>
