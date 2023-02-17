<template>
  <div>
    <ul>
      <li v-for="event in events" :key="event.id">
        {{ event.title }}
        {{event.id}}
        {{event.creator}}
        <button class="delete-btn" @click="deleteEvent(event.id)">Delete</button>

        <button class="update-btn">Update</button>
      </li>
    </ul>
  </div>
</template>
<style>
.delete-btn {
  background-color: #f64f4f;
  color: white;
  padding: 0.5em 1em;
  border-radius: 5px;
  border: none;
  cursor: pointer;
  margin-right: 1em;
}

.update-btn {
  background-color: #bbbb9b;
  color: black;
  padding: 0.5em 1em;
  border-radius: 5px;
  border: none;
  cursor: pointer;
}
</style>
<script>
import axios from 'axios';

export default {
  data() {
    return {
      events: []
    };
  },
  mounted() {
    this.fetchEvents();
  },
  methods: {
    fetchEvents() {
      axios.get('http://localhost:8080/')
          .then(response => {
            this.events = response.data;
          })
          .catch(error => {
            console.error(error);
          });
    },
    deleteEvent(eventId) {
      const token = localStorage.getItem('token');
      axios.delete(`http://localhost:8080/event/${eventId}`, {
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