# 🗞️ Vue 3 News Reader App

A modern, responsive News Reader built with **Vue 3**, **TypeScript**, and **Tailwind CSS**, using the free [GNews API](https://gnews.io/) to fetch live news articles by category or keyword search.

---

## 🚀 Features

- 🔎 Search news articles by keyword
- 📰 View top headlines by category (e.g., Technology, Health, Sports)
- 🌐 External links to full news articles
- 🎨 Fully responsive UI with Tailwind CSS
- ⚡ Built with Vite for lightning-fast development
- ✅ Includes image fallback logic for blocked/broken images

---

## 🛠️ Tech Stack

- [Vue 3 + TypeScript](https://vuejs.org/)
- [Tailwind CSS](https://tailwindcss.com/)
- [GNews API](https://gnews.io/)
- [Vite](https://vitejs.dev/)

---

## 🔧 Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/ChamikaraM/fnews.git
```

### 2. Install dependencies

```bash
npm install
```

### 3. Set your GNews API key

Create a `.env` file in the root:

```bash
VITE_GNEWS_API_KEY=your_gnews_api_key_here
```

> 🔐 Get a free API key from [https://gnews.io/](https://gnews.io/)

### 4. Run the app

```bash
npm run dev
```

---

## 📦 Build for production

```bash
npm run build
```

Then deploy the `dist/` folder using Vercel, Netlify, or Firebase Hosting.

---

## 🌐 Live Demo

> 🔗 [Demo](https://fnewsreader.netlify.app/)

---

## 📁 Folder Structure

```
src/
├── assets/                # Static assets (logo, fallback images)
├── components/            # Vue components (e.g., NewsCard.vue)
├── views/                 # View components (optional)
├── App.vue                # Main UI logic
├── main.ts                # App entry point
└── ...
```

---

## ❗ Notes

- The free GNews API tier has **100 requests/day**.
- Some image links may be blocked (403) due to hotlinking
