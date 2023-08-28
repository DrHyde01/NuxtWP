<script setup lang="ts">
  const props = defineProps<{
    post: Record<'title' | 'date' | 'excerpt' | 'uri', string>
  }>();
</script>

<template>
  <NuxtLink :to="post.uri">
    <div class="items-start bg-teal-100 p-4 space-y-2 hover:shadow-md ease-in-out duration-300">
      <h2 class="font-semibold text-lg">{{post.title}}</h2>
      <p class="font-thin text-sm">{{ new Date(post.date).toLocaleDateString()}}</p>
    </div>
  </NuxtLink>
</template>