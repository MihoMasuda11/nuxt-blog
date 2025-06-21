<script setup lang="ts">
const posts = await queryCollection("blog").order("date", "DESC").all();
</script>

<template>
  <div class="text-center">
    <div class="h-[200px] flex items-center justify-center">
      <h1 class="text-4xl font-bold">mm dev.log[WIP]</h1>
    </div>
    <ul class="mt-8 space-y-4">
      <li v-for="post in posts" :key="post.id">
        <NuxtLink :to="post.path">{{ post.title }}</NuxtLink>
      </li>
    </ul>
  </div>
</template>
