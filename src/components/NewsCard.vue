<template>
  <div class="bg-white shadow rounded-xl p-4 hover:shadow-lg transition">
    <img :src="article.image" alt="" class="w-full h-48 object-cover rounded-md mb-2" />
    <h2 class="text-lg font-semibold">{{ article.title }}</h2>
    <p class="text-sm text-gray-600">{{ article.description }}</p>
    <a :href="article.url" target="_blank" class="text-indigo-800 mt-2 inline-block">Read more</a>
  </div>
</template>

<script setup>
defineProps(['article'])
</script>
