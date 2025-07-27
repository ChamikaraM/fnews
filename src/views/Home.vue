<script setup>
import { ref, onMounted } from 'vue'

const apiKey = 'YOUR_API_KEY'
const articles = ref([])
const category = ref('technology')

const fetchNews = async () => {
  const res = await fetch(
    `https://gnews.io/api/v4/top-headlines?token=${apiKey}&lang=en&topic=${category.value}`,
  )
  const data = await res.json()
  articles.value = data.articles
}

onMounted(fetchNews)
</script>

<template>
  <div class="p-4">
    <h1 class="text-2xl font-bold mb-4">Top {{ category }} News</h1>

    <select v-model="category" @change="fetchNews" class="mb-4 p-2 border rounded">
      <option value="technology">Technology</option>
      <option value="sports">Sports</option>
      <option value="health">Health</option>
      <option value="business">Business</option>
    </select>

    <div class="grid gap-4 md:grid-cols-2 lg:grid-cols-3">
      <NewsCard v-for="article in articles" :key="article.url" :article="article" />
    </div>
  </div>
</template>

<script>
import NewsCard from '../components/NewsCard.vue'
</script>
