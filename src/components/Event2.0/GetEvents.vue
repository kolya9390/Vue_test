<template>
  <div>
    <button @click="toggleCreateEvent">Создать событие</button>
    <create-event v-if="isCreateEventVisible" @close="hideCreateEvent" @eventCreated="fetchEvents" />
    <!-- остальной контент -->
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
          <!-- Добавлен атрибут maxlength для ограничения количества символов в описании события -->
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
    <div class="row card-container">
      <div v-for="event in events" :key="event.id" class="col-sm-12 col-md-6 col-lg-4 card mb-4">
        <div v-if="!editingEvent">

          <div class="card-content">
            <h3 class="card-title mb-1">{{ event.title.substring(0, 50) }}</h3>
            <p class="card-text">{{ event.description}}</p>
            <!-- Добавлено ограничение на количество символов в описании события -->
          </div>
          <div class="tags">
            <span class="tag" v-for="tag in event.tags" :key="tag">{{ tag }}</span>
          </div>



          <p class="card-location mb-2">{{ event.location }}</p>

          <div class="card-creator">Создатель: {{ event.creator }}</div>

          <div class="card-buttons">


            <button class="delete-btn" @click="deleteEvent(event._id)">
              Удалить
            </button>
            <button class="update-btn" @click="startEdit(event)">
              Редактировать
            </button>
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
.card-container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1rem;
}

.card {
  margin-bottom: 20px;
  background-color: white;
  box-shadow: 0 0.25rem 0.5rem rgba(0, 0, 0, 0.15);
  border: 1px solid #ccc;
  border-radius: 5px;
  overflow: hidden;
}

.card-content {
  padding: 1rem;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  height: 100%;
}

.card-title {
  margin-top: 0;
  font-size: 1.2rem;
}

.card-text {
  margin-bottom: 1rem;
  max-height: 5.5rem;
  overflow: hidden;
}

.tags {
  display: flex;
  flex-wrap: wrap;
  margin-top: 10px;
}

.tag {
  background-color: #efc9c9;
  border-radius: 10px;
  color: #333;
  font-size: 14px;
  font-weight: 500;
  margin-right: 5px;
  margin-bottom: 5px;
  padding: 5px 10px;
  cursor: pointer;
}

.tag:hover {
  background-color: #333;
  color: #fff;
}


.card-location {
  margin-bottom: 0.5rem;
}

.card-creator {
  font-size: 0.8rem;
  margin-bottom: 0.5rem;
  color: #777;
}

.card-buttons {
  display: flex;
  justify-content: flex-end;
  align-items: center;
}

.delete-btn {
  background-color: #f64f4f;
  color: white;
  padding: 0.5em 1em;
  border-radius: 5px;
  border: none;
  cursor: pointer;
  margin-left: 0.5rem;
}

.update-btn {
  background-color: #007bff;
  color: white;
  padding: 0.5em 1em;
  border-radius: 5px;
  border: none;
  cursor: pointer;
  margin-left: 0.5rem;
}
</style>