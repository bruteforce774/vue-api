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
import axios from 'axios';

const posts = ref([]);

onMounted(async () => {
  const res = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=5');
  posts.value = res.data;
});
</script>

