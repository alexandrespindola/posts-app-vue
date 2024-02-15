<script setup>

import { ref, onMounted } from 'vue'
import BlogPost from './components/BlogPost.vue'
import PaginatePost from './components/PaginatePost.vue';
import LoadingSpinner from './components/LoadingSpinner.vue'
import { capitalize } from './utils/functions.js'

const posts = ref([])
const postXpage = 10
const start = ref(0)
const end = ref(postXpage)
const loading = ref(false)

const favorite = ref('')

const changeFavorite = (title) => {
    favorite.value = title
}

const next = () => {
    start.value += postXpage
   end.value += postXpage
}

const prev = () => {
    start.value -= postXpage
   end.value -= postXpage
}

onMounted(async() => {
  loading.value = true
  try {
    const rest = await fetch('https://jsonplaceholder.typicode.com/posts')
    posts.value = await rest.json()
  } catch (error) {
    console.error('Error:', error)
  }
  finally {
    loading.value = false
  }
  
})

</script>

<template>
  <main class="d-flex flex-column justify-content-center">
    <div>
      <h1 class="container-fluid text-bg-primary text-center pt-5 pb-5">Posts App Vue + Bootstrap</h1>
      <h2 class="p-4 text-center">My Favorite Post: {{ capitalize(favorite) }}</h2>

      <PaginatePost 
        @next="next" 
        @prev="prev" 
        :start="start" 
        :end="end" 
        :maxLength="posts.length"
      />

    </div>
    <div class="container d-flex flex-row flex-wrap justify-content-center gap-3 pb-4">
      <p class="m-1 text-primary text-center w-100">Choose your favorite post</p>
    </div>
    <LoadingSpinner v-if="loading"/>
    <div v-else class="container d-flex flex-row gap-3 justify-content-center flex-wrap">
      <BlogPost 
        v-for="post in posts.slice(start, end)"
        :title="post.title"
        :id="post.id"
        :subtitle="post.subtitle"
        @changeFavoriteName="changeFavorite"
      />
    </div>
  </main>
</template>