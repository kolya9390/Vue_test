<template>
  <div>
    <button class="btn btn-primary mb-3" @click="toggleCreateEvent">Создать событие</button>
    <create-event v-if="isCreateEventVisible" @close="hideCreateEvent" @eventCreated="fetchEvents" />
  </div>
  <div class="container">
    <div v-if="editingEvent">
      <form class="edit-form">
        <div class="form-group">
          <label for="edit-title">Заголовок</label>
          <input id="edit-title" v-model="editedEvent.title" type="text" class="form-control" autocomplete="off"/>
        </div>
        <div class="form-group">
          <label for="edit-description">Описание</label>
          <textarea id="edit-description" v-model="editedEvent.description" class="form-control" autocomplete="off" maxlength="150"></textarea>
        </div>
        <div class="form-group">
          <label for="edit-location">Место проведения</label>
          <input id="edit-location" v-model="editedEvent.location" type="text" class="form-control" autocomplete="off"/>
        </div>
        <div class="edit-form-buttons">
          <button class="btn btn-primary" @click.prevent="saveEvent" aria-label="Сохранить событие">Сохранить</button>
          <button class="btn btn-secondary" @click.prevent="cancelEdit">Отмена</button>
        </div>
      </form>
    </div>
    <div class="row">
      <div v-for="event in events" :key="event.id" class="col-sm-12 col-md-6 col-lg-4 mb-4">
        <div v-if="!editingEvent" class="card h-100">
          <div class="card-body">
            <h5 class="card-title mb-1">{{ event.title.substring(0, 50) }}</h5>
            <p class="card-text">{{ event.description}}</p>
            <div class="d-flex flex-wrap align-items-center justify-content-between">
              <div class="tags mb-2">
                <span class="badge badge-secondary mr-1 mb-1" v-for="tag in event.tags" :key="tag">{{ tag }}</span>
              </div>
              <p class="card-location mb-2">{{ event.location }}</p>
            </div>
            <div class="card-creator">Создатель: {{ event.creator }}</div>
          </div>
          <div class="card-footer d-flex justify-content-end">
            <button class="btn btn-danger mr-2" @click="deleteEvent(event._id)">Удалить</button>
            <button class="btn btn-primary" @click="startEdit(event)">Редактировать</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>


<script>
import axios from 'axios';
import CreateEvent from "@/components/Event2.0/Create_Event.vue";

export default {
  components: {
    CreateEvent
  },
  data() {
    return {
      isCreateEventVisible: false,
      events: [],
      editingEvent: null,
      editedEvent: null
    };
  },
  created() {
    this.fetchEvents()
  },
  methods: {
    async fetchEvents() {
      try {
        const response = await axios.get('http://localhost:8080/event');
        this.events = response.data;
      } catch (error) {
        console.error(error);
      }
    },
    async deleteEvent(eventId) {
      try {
        const token = localStorage.getItem('token');
        await axios.delete(`http://localhost:8080/event/${eventId}`,{
          headers: {
            Authorization: `Bearer ${token}`
          }
        });

        await this.fetchEvents();
      } catch (error) {
        console.error(error);
      }
    },
    toggleCreateEvent() {
      this.isCreateEventVisible = !this.isCreateEventVisible;
    },
    hideCreateEvent() {
      this.isCreateEventVisible = false;
    },
    startEdit(event) {
      this.editingEvent = event;
      this.editedEvent = Object.assign({}, event);
    },
    cancelEdit() {
      this.editingEvent = null;
      this.editedEvent = null;
    },
    async saveEvent() {
      try {
        const token = localStorage.getItem('token');
        await axios.put(
            `http://localhost:8080/event/${this.editedEvent._id}`,
            this.editedEvent,
            {
              headers: {
                Authorization: `Bearer ${token}`
              }
            }
        );
        this.editingEvent.title = this.editedEvent.title;
        this.editingEvent.description = this.editedEvent.description;
        this.editingEvent.location = this.editedEvent.location;
        this.editingEvent = null;
        this.editedEvent = null;
      } catch (error) {
        console.error(error);
      }
    },


  }
};
</script>



<style>
.card {
  height: 400px; /* задаем фиксированную высоту карточки */
}
</style>