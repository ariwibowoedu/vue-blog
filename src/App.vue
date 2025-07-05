<script setup>
import { RouterView } from 'vue-router'
import NavbarSec from '@/components/navigations/NavbarSec.vue'
</script>

<template>
  <div class="min-h-screen">
    <NavbarSec />
    <RouterView />
  </div>
</template>
