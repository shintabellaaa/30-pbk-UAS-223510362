<script setup>
import { ref } from 'vue';
import Todos from './components/Todos.vue';
import Post from './components/Post.vue';
import AlbumFoto from './components/AlbumFoto.vue';

const selectedMenu = ref('');

const handleMenuClick = (menu) => {
  selectedMenu.value = menu;
};
</script>

<template>
  <div>
    <button @click="handleMenuClick('Todos')">Todos</button>
    <button @click="handleMenuClick('Post')">Post</button>
    <button @click="handleMenuClick('AlbumFoto')">Album Foto</button>

    <div>
      <!-- Menampilkan komponen Todos jika menu Todos dipilih -->
      <Todos v-if="selectedMenu === 'Todos'" />

      <!-- Menampilkan komponen Post jika menu Post dipilih -->
      <Post v-if="selectedMenu === 'Post'" />

      <!-- Menampilkan komponen AlbumFoto jika menu AlbumFoto dipilih -->
      <AlbumFoto v-if="selectedMenu === 'AlbumFoto'" />

      <!-- Pesan ketika tidak ada menu yang dipilih -->
      <p v-if="!selectedMenu.value">No menu selected</p>
    </div>
  </div>
</template>
