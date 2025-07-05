<script setup>
import { useRoute } from 'vue-router'
import { posts } from '@/data/posts'

const route = useRoute()
const post = posts.find((p) => p.id === route.params.id)
</script>


<template>
  <div class="p-4">
    <div v-if="post">
      <h1 class="text-xl font-bold">{{ post.title }}</h1>
      <p class="text-sm text-gray-500">{{ post.date }}</p>
      <div class="mt-4 text-gray-800 whitespace-pre-line">
        {{ post.content }}
      </div>
    </div>
    <div v-else>
      <h1 class="text-2xl text-red-500">Post Not Found.</h1>
    </div>
  </div>
</template>

<style>
</style>