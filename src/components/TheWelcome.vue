<template>
  <div class="p-4">
    <h1 class="text-3xl">Bienvenue chez GIE HOLDING GROUP DIAMA</h1>
    <p class="my-4">Lorem ipsum dolor sit amet consectetur adipisicing elit.</p>

    <ul class="flex flex-col gap-4">
      <li>
        <RouterLink to="/new-facture" class="flex items-center">
          <span class="text-lg">Nouvelle Facture</span>
          <IconPlus />
        </RouterLink>
      </li>
    </ul>
  </div>
</template>

<script setup>
  import { RouterLink } from 'vue-router'
  import IconPlus from '@/components/icons/IconPlus.vue'
</script>

