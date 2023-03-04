<template>
  <div class="create-event">
    <h1 class="mb-4">Create Event</h1>
    <form @submit.prevent="submitForm" class="w-50">
      <div class="form-group">
        <label for="title" class="form-label">Title</label>
        <input type="text" id="title" v-model="title" required class="form-control">
      </div>

      <div class="form-group">
        <label for="description" class="form-label">Description</label>
        <textarea id="description" v-model="description" required class="form-control"></textarea>
      </div>
      <div class="form-group">
        <label for="tags" class="form-label">Tags (separated by commas)</label>
        <input type="text" id="tags" v-model="tagsInput" required class="form-control">
      </div>
      <div class="form-group">
        <label for="location" class="form-label">Location</label>
        <input type="text" id="location" v-model="location" required class="form-control">
      </div>
      <button type="submit" class="btn btn-primary submit-btn mt-3">Create Event</button>
    </form>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      title: '',
      image: '',
      description: '',
      tags: [],
      location: '',
      tagsInput: ''
    };
  },
  methods: {
    async submitForm() {
      const token = localStorage.getItem('token');
      const tags = this.tagsInput.split(',').map(tag => tag.trim());
      axios.post(`http://localhost:8080/event/new`, {
        title: this.title,
        image: this.image,
        description: this.description,
        tags: tags.concat(this.tags.filter(tag => !tags.includes(tag))), // объединяем новые теги и старые теги
        location: this.location
      }, {
        headers: {
          Authorization: `Bearer ${token}`
        }
      })
          .then(response => {
            this.$emit('eventCreated', response.data.event); // эмитируем событие eventCreated и передаем созданное событие
            this.title = '';
            this.image = '';
            this.description = '';
            this.tags = [];
            this.location = '';
            this.tagsInput = '';
            this.$router.push('/'); // Добавляем редирект на страницу /event
            this.fetchEvents(); // вызываем метод fetchEvents() для обновления списка событий
          })
          .catch(error => {
            console.error(error);
          });
    }
  }
};
</script>


<style>
.create-event {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 50px;
}

.form-group {
  margin-bottom: 20px;
  width: 100%;
}

label {
  font-weight: bold;
}

input,
textarea {
  border-radius: 5px;
}

.submit-btn {
  border-radius: 5px;
  font-weight: bold;
}

.submit-btn:hover {
  background-color: #357ae8;
}

.submit-btn:active {
  background-color: #4d90fe;
}
</style>