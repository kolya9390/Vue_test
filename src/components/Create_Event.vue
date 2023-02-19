<template>
  <div>
    <h1>Create Event</h1>
    <form @submit.prevent="createEvent">
      <label for="title">Title</label>
      <input type="text" id="title" v-model="event.title" required>
      <label for="image">Image URL</label>
      <input type="text" id="image" v-model="event.image" required>

      <label for="description">Description</label>
      <textarea id="description" v-model="event.description" required></textarea>

      <label for="tags">Tags (separated by commas)</label>
      <input type="text" id="tags" v-model="tagsInput" required>

      <label for="location">Location</label>
      <input type="text" id="location" v-model="event.location" required>

      <button type="submit">Create Event</button>
    </form>
  </div>
</template>
<script>
import axios from 'axios';

export default {
  data() {
    return {
      event: {
        title: '',
        image: '',
        description: '',
        tags: [],
        location: '',
      },
      tagsInput: ''
    };
  },
  methods: {
    async createEvent() {
      const token = localStorage.getItem('token');
      const tags = this.tagsInput.split(',').map(tag => tag.trim());
      axios.post(`http://localhost:8080/event/new`, {
        title: this.event.title,
        image: this.event.image,
        description: this.event.description,
        tags: tags.concat(this.event.tags.filter(tag => !tags.includes(tag))), // объединяем новые теги и старые теги
        location: this.event.location
      }, {
        headers: {
          Authorization: `Bearer ${token}`
        }
      })
          .then(response => {
            this.fetchEvents();
          })
          .catch(error => {
            console.error(error);
          });
    }
  }
};
</script>
