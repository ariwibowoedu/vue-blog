<script setup>
defineProps({
  post: Object,
})
</script>


<template>
  <div class="bg-white p-4 shadow rounded hover:shadow-md transition">
    <router-link
      :to="`/post/${post.id}`"
      class="text-xl font-semibold text-blue-500 hover:underline"
    >
      {{ post.title }}
    </router-link>
    <p class="text-sm text-gray-500">{{ post.date }} — {{ post.category }}</p>
    <p class="mt-2 text-gray-700">{{ post.excerpt }}</p>
  </div>
</template>

<style>
</style>