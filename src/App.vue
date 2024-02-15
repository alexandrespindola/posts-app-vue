<script setup>

import { ref } from 'vue'
import BlogPost from './components/BlogPost.vue'
import PaginatePost from './components/PaginatePost.vue';
import { capitalize } from './utils/functions.js'

const posts = ref([])
const postXpage = 10
const start = ref(0)
const finish = ref(postXpage)

const favorite = ref('')

const changeFavorite = (title) => {
    favorite.value = title
}

const next = () => {
    start.value += postXpage
    finish.value += postXpage
}

const prev = () => {
    start.value -= postXpage
    finish.value -= postXpage
}

fetch('https://jsonplaceholder.typicode.com/posts')
    .then(response => response.json())
    .then(data => posts.value = data)    
    .catch(error => console.error('Error:', error)
    )
</script>

<template>
  <main class="d-flex flex-column justify-content-center">
    <div>
      <h1 class="container-fluid text-bg-primary text-center pt-5 pb-5">APP Posts Vue + Bootstrap</h1>
      <h2 class="pt-4 pb-4 text-center">My Favorite Post: {{ capitalize(favorite) }}</h2>

      <PaginatePost @next="next" @prev="prev" />

    </div>
    <div class="container d-flex flex-row flex-wrap justify-content-center gap-3 pb-4">
      <p class="m-1 text-primary text-center w-100">Choose your favorite post</p>
    </div>
    <div class="container d-flex flex-row gap-3 justify-content-center flex-wrap">
      <BlogPost 
        v-for="post in posts.slice(start, finish)"
        :title="post.title"
        :id="post.id"
        :subtitle="post.subtitle"
        @changeFavoriteName="changeFavorite"
      />
    </div>
  </main>
</template>