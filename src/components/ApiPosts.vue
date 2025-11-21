<template>
  <div>
    <h2>Posts from JSONPlaceholder</h2>
    <form @submit.prevent="addPost">
      <input v-model="newTitle" placeholder="Title" required />
      <input v-model="newBody" placeholder="Body" required />
      <button type="submit">Add Post</button>
    </form>
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
const newTitle = ref('');
const newBody = ref('');

onMounted(async () => {
  const res = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=5');
  posts.value = res.data;
});

async function addPost() {
  const postData = {
    title: newTitle.value,
    body: newBody.value,
    userId: 1
  };
  const res = await axios.post('https://jsonplaceholder.typicode.com/posts', postData);
  // For demo: add the new post to the top of the list
  posts.value.unshift(res.data);
  newTitle.value = '';
  newBody.value = '';
}
</script>

