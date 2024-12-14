<script setup>
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue'
</script>

<template>
  <nav class="bg-white shadow">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="flex justify-between h-16">
        <div class="flex">
          <RouterLink class="flex-shrink-0" to="/">
            <img alt="Vue logo" class="h-16 w-auto" src="./assets/logo.png" />
          </RouterLink>
          <div class="hidden sm:ml-6 sm:flex sm:space-x-8">
            <RouterLink class="border-blue-500 text-gray-900 inline-flex items-center px-1 pt-1 border-b-2 text-sm font-medium" to="/">Accueil</RouterLink>
            <RouterLink class="border-transparent text-gray-500 hover:text-gray-700 hover:border-gray-300 inline-flex items-center px-1 pt-1 border-b-2 text-sm font-medium" to="/about">Factures</RouterLink>
          </div>
        </div>
      </div>
    </div>
  </nav>

  <RouterView />
</template>

<style scoped>
</style>
