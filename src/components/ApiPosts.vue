<template>
  <div>
    <h2>Posts from JSONPlaceholder</h2>
    <ul v-if="posts.length">
      <li v-for="post in posts" :key="post.id">
        <strong>{{ post.title }}</strong>
        <p>{{ post.body }}</p>
      </li>
    </ul>
    <p v-else>Loading...</p>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';

const posts = ref([]);

onMounted(async () => {
  const res = await fetch('https://jsonplaceholder.typicode.com/posts?_limit=5');
  posts.value = await res.json();
});
</script>

