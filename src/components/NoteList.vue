<template>
  <div class="note-list">
    <ul class="list-group">
      <li v-for="(note, index) in notes" :key="note.id" class="list-group-item mb-3">
        <div class="card p-3 shadow-sm">
          <h5 class="note-title">{{ note.title }}</h5>
          <p class="note-content">{{ note.text }}</p>
          <p class="note-date">{{ note.date }}</p>
          <div class="d-flex justify-content-between">
            <button @click="editNote(note)" class="btn btn-warning btn-sm">Редактировать</button>
            <button @click="deleteNote(index)" class="btn btn-danger btn-sm">Удалить</button>
          </div>
        </div>
      </li>
    </ul>
    <button @click="clearNotes" class="btn btn-danger mt-3">Очистить все заметки</button>
  </div>
</template>

<script>
export default {
  name: 'NoteList',
  props: {
    notes: Array,
  },
  methods: {
    deleteNote(index) {
      this.$emit('delete-note', index);
    },
    editNote(note) {
      const newTitle = prompt('Редактировать заголовок заметки', note.title);
      const newText = prompt('Редактировать содержание заметки', note.text);
      if (newTitle && newText && (newTitle !== note.title || newText !== note.text)) {
        this.$emit('edit-note', { ...note, title: newTitle, text: newText });
      }
    },
    clearNotes() {
      if (confirm('Вы уверены, что хотите очистить все заметки?')) {
        this.$emit('clear-notes');
      }
    },
  },
};
</script>

<style scoped>
.note-list {
  margin-top: 30px;
}

.card {
  border-radius: 10px;
  background-color: #ffffff;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
}

.note-title {
  font-family: 'Georgia', serif;
  font-size: 1.5rem;
  color: #4b2e83;
}

.note-content {
  font-family: 'Courier New', Courier, monospace;
  font-size: 1.2rem;
  color: #333;
}

.note-date {
  font-size: 0.9rem;
  color: #777;
  font-style: italic;
  margin-top: 10px;
}

button {
  border-radius: 5px;
}
</style>
