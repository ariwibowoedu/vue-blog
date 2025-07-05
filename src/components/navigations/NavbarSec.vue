<template>
  <div class="bg-gray-100">
    <nav class="bg-white shadow px-4 py-2 mb-4">
      <router-link to="/" class="mr-4">Home</router-link>
      <router-link to="/about" class="mr-4">About</router-link>
    </nav>
  </div>
</template>

<script setup>
import { RouterLink } from 'vue-router'
</script>

<style>
</style>