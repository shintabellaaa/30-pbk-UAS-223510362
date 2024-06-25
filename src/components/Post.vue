<template>
    <div>
      <h2>Post</h2>
      <select v-model="selectedUser" @change="fetchPosts" class="select-user">
        <option value="">Select User</option>
        <option v-for="user in users" :key="user.id" :value="user.id">{{ user.name }}</option>
      </select>
      <ul v-if="posts.length" class="post-list">
        <li v-for="post in posts" :key="post.id" class="post-item">
          <h3>{{ post.title }}</h3>
          <p>{{ post.body }}</p>
        </li>
      </ul>
      <p v-else-if="selectedUser && !posts.length" class="no-posts">No posts available for this user</p>
      <p v-else class="no-posts">No posts available</p>
    </div>
  </template>
  
  <script setup>
  import { ref, onMounted } from 'vue';
  
  const users = ref([]);
  const selectedUser = ref('');
  const posts = ref([]);
  
  const fetchUsers = async () => {
    try {
      const response = await fetch(`https://jsonplaceholder.typicode.com/users`);
      const data = await response.json();
      users.value = data;
    } catch (error) {
      console.error('Error fetching users:', error);
    }
  };
  
  const fetchPosts = async () => {
    try {
      if (!selectedUser.value) return;
      const response = await fetch(`https://jsonplaceholder.typicode.com/posts?userId=${selectedUser.value}`);
      const data = await response.json();
      posts.value = data;
    } catch (error) {
      console.error('Error fetching posts:', error);
    }
  };
  
  onMounted(() => {
    fetchUsers();
  });
  </script>
  