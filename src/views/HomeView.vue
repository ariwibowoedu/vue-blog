<script setup>
import PostCard from '@/components/posts/PostCard.vue'
import { computed, ref } from 'vue'
import { posts } from '@/data/posts'

const searchQuery = ref('')
const selectedCategory = ref('All')
const currentPage = ref(1)
const postsPerPage = 3

const categories = ['All', ...new Set(posts.map((post) => post.category))]

const filteredPosts = computed(() => {
  return posts.filter((post) => {
    const matchesSearch = post.title.toLowerCase().includes(searchQuery.value.toLowerCase())
    const matchesCategory =
      selectedCategory.value === 'All' || post.category === selectedCategory.value
    return matchesSearch && matchesCategory
  })
})

const totalPages = computed(() => Math.ceil(filteredPosts.value.length / postsPerPage))

const paginatedPosts = computed(() => {
  const start = (currentPage.value - 1) * postsPerPage
  return filteredPosts.value.slice(start, start + postsPerPage)
})

const goToPage = (page) => {
  if (page >= 1 && page <= totalPages.value) {
    currentPage.value = page
  }
}
</script>

<template>
  <div class="p-4">
    <h1 class="text-2xl font-bold mb-4">Latest Posts</h1>

    <div class="flex flex-col md:flex-row gap-4 mb-6">
      <input
        type="text"
        v-model="searchQuery"
        placeholder="Search posts..."
        class="p-2 border rounded w-full md:w-1/2"
      />

      <select v-model="selectedCategory" class="p-2 border rounded w-full md:w-1/2">
        <option v-for="cat in categories" :key="cat" :value="cat">{{ cat }}</option>
      </select>
    </div>
    <div class="grid gap-4">
      <post-card v-for="post in paginatedPosts" :key="post.id" :post="post" />
    </div>
    <div v-if="totalPages > 1" class="mt-6 flex gap-2">
      <button
        @click="goToPage(currentPage - 1)"
        :disabled="currentPage === 1"
        class="px-3 py-1 bg-gray-200 rounded hover:bg-gray-300 disabled:opacity-50"
      >
        Prev
      </button>
      <button
        v-for="page in totalPages"
        :key="page"
        @click="goToPage(page)"
        :class="[
          'px-3 py-1 rounded',
          currentPage === page ? 'bg-blue-500 text-white' : 'bg-gray-200 hover:bg-gray-300',
        ]"
      >
        {{ page }}
      </button>
      <button
        @click="goToPage(currentPage + 1)"
        :disabled="currentPage === totalPages"
        class="px-3 py-1 bg-gray-200 rounded hover:bg-gray-300 disabled:opacity-50"
      >
        Next
      </button>
    </div>
  </div>
</template>
