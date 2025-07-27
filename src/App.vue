<template>
  <div class="min-h-screen bg-gradient-to-b from-gray-100 to-white text-gray-900">
    <header class="bg-white shadow sticky top-0 z-10">
      <div class="container mx-auto px-4 py-4 flex justify-between items-center">
        <h1 class="text-2xl sm:text-3xl font-bold text-indigo-800">🗞️ News Reader</h1>
        <span class="text-sm text-gray-500">Powered by GNews API</span>
      </div>
    </header>

    <main class="container mx-auto px-4 py-8">
      <div class="flex flex-col sm:flex-row items-center gap-4 mb-6">
        <select
          v-model="category"
          @change="fetchNews"
          class="p-2 border border-gray-300 rounded-lg shadow-sm focus:outline-none focus:ring focus:ring-blue-200 w-full sm:w-auto"
        >
          <option value="technology">Technology</option>
          <option value="sports">Sports</option>
          <option value="health">Health</option>
          <option value="business">Business</option>
          <option value="world">World</option>
        </select>

        <input
          v-model="query"
          @keyup.enter="fetchNews"
          type="text"
          placeholder="Search news articles..."
          class="p-2 border border-gray-300 rounded-lg shadow-sm w-full sm:w-1/2 focus:outline-none focus:ring focus:ring-blue-200"
        />
      </div>

      <div
        v-if="loading"
        class="text-center text-lg font-medium py-10 animate-pulse text-indigo-800"
      >
        Loading news articles...
      </div>

      <div v-else-if="articles.length === 0" class="text-center text-gray-600 py-10">
        No articles found. Try a different keyword or category.
      </div>

      <div v-else class="grid gap-8 md:grid-cols-2 lg:grid-cols-3">
        <div
          v-for="article in articles"
          :key="article.url"
          class="bg-white rounded-2xl shadow-md overflow-hidden transform hover:scale-[1.02] hover:shadow-xl transition duration-300"
        >
          <img
            :src="article.image"
            @error="
              (e) => {
                if (e.target) (e.target as HTMLImageElement).src = fallbackImage
              }
            "
            alt="News image"
            class="w-full h-48 object-cover"
            v-if="article.image"
          />
          <div class="p-4 flex flex-col h-full">
            <h2 class="text-lg font-semibold mb-2 line-clamp-2">{{ article.title }}</h2>
            <p class="text-sm text-gray-600 mb-3 line-clamp-3">{{ article.description }}</p>
            <a
              :href="article.url"
              target="_blank"
              class="text-indigo-800 font-medium hover:underline"
            >
              Read more →
            </a>
          </div>
        </div>
      </div>
    </main>

    <footer class="mt-12 text-center text-sm text-gray-500 pb-8">
      Made by CMT using Vue 3 & Tailwind CSS
    </footer>
  </div>
</template>

<script lang="ts" setup>
import { ref, onMounted } from 'vue'
import fallbackImage from '@/assets/fallbackimage.jpg'

const apiKey = import.meta.env.VITE_GNEWS_API_KEY
const category = ref('technology')
const query = ref('')
const articles = ref<any[]>([])
const loading = ref(false)

const fetchNews = async () => {
  loading.value = true
  try {
    const url =
      query.value.trim() !== ''
        ? `https://gnews.io/api/v4/search?q=${encodeURIComponent(query.value)}&token=${apiKey}&lang=en`
        : `https://gnews.io/api/v4/top-headlines?token=${apiKey}&lang=en&topic=${category.value}`

    const res = await fetch(url)
    const data = await res.json()
    articles.value = data.articles
  } catch (error) {
    console.error('Error fetching news:', error)
    articles.value = []
  } finally {
    loading.value = false
  }
}

onMounted(fetchNews)
</script>

<style>
/* Optional: clamp for multi-line truncation */
.line-clamp-2 {
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

.line-clamp-3 {
  display: -webkit-box;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
  overflow: hidden;
}
</style>
