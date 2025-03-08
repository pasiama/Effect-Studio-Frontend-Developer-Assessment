<template>
      <div class="bg-white rounded-xl shadow-lg overflow-hidden ml-8 mr-8 mb-4">
    
        <div class="p-4">
          <span class="inline-block px-3 py-1 text-xs font-semibold text-white rounded-full" :class="categoryColor(article.category)">
            {{ article.category }}
          </span>
    
          <h2 class="mt-2 text-lg font-bold text-gray-900 hover:text-blue-600 transition duration-200">
            {{ article.title }}
          </h2>
    
          <p class="text-sm text-gray-500 mt-1">{{ article.date }}</p>
        </div>
        <img :src="article.image" alt="news image" class="w-full h-48 object-cover" />

      </div>
    </template>
    
    <script setup>
    defineProps({
      article: Object,
    });
    
    // Dynamically set category colors
    const categoryColor = (category) => {
      const colors = {
        "Connecting Africa": "bg-green-500",
        "Tech Labari": "bg-blue-500",
        "Techstars": "bg-teal-500",
        "Medium": "bg-green-600",
        "Futher Africa": "bg-purple-500",
        "TechCrunch": "bg-green-400",
      };
      return colors[category] || "bg-gray-500";
    };
    </script>
    