<template>
  <div>
    <div class="form-group">
      <label for="tag-filter">Фильтр по тегам</label>
      <input id="tag-filter" v-model="tagFilter" type="text" class="form-control" autocomplete="off"/>
    </div>
  </div>
  <div class="container">
    <div v-if="editingEvent">
      <!-- ... -->
    </div>
    <div class="row">
      <div v-for="event in filteredEvents" :key="event.id" class="col-sm-12 col-md-6 col-lg-4 mb-4">
        <!-- ... -->
      </div>
    </div>
  </div>
</template>
<script>
// ...
export default {
  // ...
  data() {
    return {
      isCreateEventVisible: false,
      events: [],
      editingEvent: null,
      editedEvent: null,
      tagFilter: ''
    };
  },
  computed: {
    filteredEvents() {
      if (!this.tagFilter) {
        return this.events;
      }
      const filterText = this.tagFilter.toLowerCase();
      return this.events.filter(event => {
        return event.tags.some(tag => tag.toLowerCase().includes(filterText));
      });
    }
  },
}
</script>
