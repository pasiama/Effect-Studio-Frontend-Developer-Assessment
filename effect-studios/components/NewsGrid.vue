<template>
      <section class="container mx-auto px-4 py-10">
        <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-2 ml-10 mr-10">
          <NewsCard v-for="article in articles" :key="article.id" :article="article" />
        </div>
      </section>
    </template>
    
    <script setup>
    
    const articles = [
      {
        id: 1,
        category: "Connecting Africa",
        title: "Combining AI, fintech to solve African problems – Ericsson",
        date: "December 06, 2021",
        image: "/images/facebook.png",
      },
      {
        id: 2,
        category: "Tech Labari",
        title: "Ghana to Host the 14th Africa Fintech Summit on October 8th",
        date: "May 24, 2022",
        image: "/images/africa.png",
      },
      {
        id: 3,
        category: "Techstars",
        title: "Midterm Report: Techstars Toronto’s Second 2021 Class",
        date: "Dec 06, 2021",
        image: "/images/starters.png",
      },
      {
        id: 4,
        category: "Medium",
        title: "Wise granted approval to join Zengin, Japan’s domestic payment system",
        date: "December 06, 2021",
        image: "/images/wise.png",
      },
      {
        id: 5,
        category: "Futher Africa",
        title: "African startups to participate at Techstars Toronto October 2021 cohort",
        date: "October 23, 2021",
        image: "/images/tech.png",
      },
      {
        id: 6,
        category: "TechCrunch",
        title: "More African startups get into Techstars Toronto",
        date: "October 18, 2021",
        image: "/images/tech.png",
      },
    ];
    </script>
    