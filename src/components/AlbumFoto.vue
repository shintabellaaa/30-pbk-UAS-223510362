<template>
  <div class="album">
    <div v-for="photo in photos" :key="photo.id" class="photo-item">
      <img :src="photo.url" alt="Photo">
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      photos: []
    };
  },
  mounted() {
    axios.get('https://jsonplaceholder.typicode.com/photos')
      .then(response => {
        this.photos = response.data;
      })
      .catch(error => {
        console.error('Error fetching photos:', error);
      });
  }
};
</script>

<style scoped>
.album {
  display: flex;
  flex-wrap: wrap;
}

.photo-item {
  width: 200px;
  height: 200px;
  margin: 10px;
  overflow: hidden;
}

.photo-item img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}
</style>
