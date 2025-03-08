<template>
  <div class="max-w-4xl mx-auto px-4 py-8">
    <!-- Mission Statement -->
    <h2 class="text-left text-3xl font-bold text-[#233375] mb-12 mx-4">
      We are on a mission to reduce the cost of sending<br />
      money to Africa at an average cost of 1%
    </h2>

    <div class="grid grid-cols-1 md:grid-cols-2 gap-8 items-start w-full">
      <!-- Calculator Section -->
      <div class="bg-white rounded-lg p-6 mr-8">
        <!-- Amount Input -->
        <div class="mb-4 relative">
          <p class="text-sm text-gray-500 mb-1">You send</p>

          <div
            class="relative flex items-center bg-white rounded-lg shadow-md overflow-hidden"
          >
            <input
              type="number"
              v-model="amount"
              class="text-2xl font-medium w-full p-3 border rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500 text-[#233375]"
              placeholder="0.00"
            />
            <div class="absolute right-3 top-3">
              <button
                class="flex items-center space-x-2 bg-[#233375] text-white px-3 py-1 rounded"
              >
                <img
                  src="https://flagcdn.com/w20/gb.png"
                  class="w-5 h-auto"
                  alt="UK flag"
                />
                <span>GBP</span>
              </button>
            </div>
          </div>
      
        </div>
        <div class="h-4 w-[2px] bg-gray-300 ml-3"></div>

        <!-- Fee Section -->
        <div
          class="flex items-center justify-start text-gray-500 text-sm space-x-2 mb-2"
        >
          <div
            class="w-6 h-6 rounded-full border border-gray-400 flex items-center justify-center"
          >
            <span class="text-gray-600">−</span>
          </div>
          <span>{{ feeAmount }} GBP</span>
          <select
            class="bg-gray-200 text-gray-700 px-2 py-1 rounded focus:outline-none lg:hidden"
          >
            <option>Express</option>
            <option>Standard</option>
          </select>
          <span>Fee</span>
        </div>
        <div class="h-4 w-[2px] bg-gray-300 ml-3"></div>

        <!-- Converted Amount -->
        <div class="mb-4 relative">
          <p class="text-sm text-gray-500 mb-1">You receive</p>
          <div
            class="relative flex items-center bg-white rounded-lg shadow-md overflow-hidden"
          >
            <input
              type="number"
              :value="convertedAmount"
              readonly
              class="text-2xl font-medium w-full p-3 border rounded-lg bg-gray-50 text-[#233375]"
            />
            <div class="absolute right-3 top-3">
              <button
                class="flex items-center space-x-2 bg-[#233375] text-white px-3 py-1 rounded"
              >
                <img
                  src="https://flagcdn.com/w20/gh.png"
                  class="w-5 h-auto"
                  alt="Ghana flag"
                />
                <span>GHS</span>
              </button>
            </div>
          </div>
        </div>

        <!-- Exchange Rate Info -->
        <div class="flex justify-between space-x-2 mb-4">
          <span class="text-sm text-gray-600 mr-8">Amount we'll convert</span>

          <svg
            xmlns="http://www.w3.org/2000/svg"
            class="h-5 w-5 text-green-500"
            viewBox="0 0 20 20"
            fill="currentColor"
          >
            <path
              fill-rule="evenodd"
              d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.293a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z"
              clip-rule="evenodd"
            />
          </svg>
          <span class="text-sm text-gray-600">Guaranteed rate (1hr)</span>
        </div>

        <div class="flex justify-between text-sm text-[#233375] mb-4 font-bold">
          <div>{{ feeAmount }}</div>
          <div class="flex items-center">
            <span class="mr-2">£1 = GHS{{ exchangeRate.toFixed(2) }}</span>
          </div>
        </div>

        <div class="flex justify-between space-x-2 mb-4">
          <span class="text-sm text-gray-600 mr-8">Total to Pay</span>
          <span class="text-sm text-gray-600">Average Duration</span>
        </div>

        <div class="flex justify-between text-sm text-[#233375] mb-4">
          <div class="font-bold">{{ feeAmount }} GBP</div>
          <div class="flex items-center">
            <span class="text-[#233375] font-medium">Instant</span>
          </div>
        </div>

        <!-- Total Amount -->
        <div class="border-t pt-4 mb-6">
          <div class="flex justify-between items-center">
            <span class="text-gray-600">Total to pay</span>
            <span class="text-xl font-medium text-[#233375]"
              >£{{ totalAmount }}</span
            >
          </div>
        </div>

        <!-- CTA Button -->
        <button
          class="w-full bg-[#1e3a8a] text-white py-3 rounded-lg font-medium hover:bg-blue-900 transition-colors"
        >
          Get started for free
        </button>
      </div>

      <!-- Info Section -->
      <div class="ml-8">
        <div class="mb-2 text-gray-600">Why Bomba?</div>
        <h3 class="text-3xl font-bold text-[#1e3a8a] mb-4">
          Send & Receive money on your own terms
        </h3>
        <p class="text-gray-600 leading-relaxed">
          Bomba provides you the luxury of sending money at rates that suit you.
          You can easily send and swap money between
          <span class="font-medium">GBP</span>,
          <span class="font-medium">USD</span>,
          <span class="font-medium">NGN</span> and to 20 other African countries
          using Bomba's <span class="text-green-500">Swap</span> and
          <span class="text-green-500">Express</span>
          services. Best bank rates, save time and gain more.
        </p>
      </div>
    </div>
    
  </div>
</template>

<script setup>
import { ref, computed } from "vue";

// State
const amount = ref(1000);
const exchangeRate = ref(19); // GHS to GBP rate
const feePercentage = 0.01; // 1% fee

// Computed values
const feeAmount = computed(() => {
  return (amount.value * feePercentage).toFixed(2);
});

const convertedAmount = computed(() => {
  return (amount.value * exchangeRate.value).toFixed(2);
});

const totalAmount = computed(() => {
  return (amount.value + Number(feeAmount.value)).toFixed(2);
});

// Fetch real exchange rate on component mount
onMounted(async () => {
  try {
    const response = await fetch(
      "https://api.exchangerate-api.com/v4/latest/GBP"
    );
    const data = await response.json();
    exchangeRate.value = data.rates.GHS;
  } catch (error) {
    console.error("Failed to fetch exchange rate:", error);
    // Fallback to default rate
  }
});
</script>

<style scoped>
input[type="number"]::-webkit-inner-spin-button,
input[type="number"]::-webkit-outer-spin-button {
  -webkit-appearance: none;
  margin: 0;
}
input[type="number"] {
  -moz-appearance: textfield;
}
</style>
