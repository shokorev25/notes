<template>
  <div class="book-cover">
    <div class="container mt-5">
      <h1 class="text-center mb-4">Заметки</h1>
      <NoteForm @add-note="addNote" />
      <NoteList
        :notes="notes"
        @delete-note="deleteNote"
        @edit-note="editNote"
        @clear-notes="clearNotes"
      />
    </div>
  </div>
</template>

<script>
import NoteForm from './components/NoteForm.vue';
import NoteList from './components/NoteList.vue';
import { saveNotes, loadNotes } from './storage.js';

export default {
  name: 'App',
  components: {
    NoteForm,
    NoteList,
  },
  data() {
    return {
      notes: loadNotes(),
    };
  },
  methods: {
    addNote(newNote) {
      this.notes.push(newNote);
      saveNotes(this.notes);
    },
    deleteNote(index) {
      this.notes.splice(index, 1);
      saveNotes(this.notes);
    },
    editNote(updatedNote) {
      this.notes = this.notes.map(note =>
        note.id === updatedNote.id ? updatedNote : note
      );
      saveNotes(this.notes);
    },
    clearNotes() {
      this.notes = [];
      saveNotes(this.notes);
    },
  },
};
</script>

<style scoped>
.book-cover {
  background: url('https://www.transparenttextures.com/patterns/old-wall-1.png') repeat, url('https://www.transparenttextures.com/patterns/wood-pattern.png') repeat;
  background-size: cover;
  padding: 50px 0;
  border-radius: 12px;
  box-shadow: inset 0 0 30px rgba(0, 0, 0, 0.3);
}

.container {
  max-width: 800px;
  background-color: #fff5e6;
  border-radius: 15px;
  box-shadow: 0 10px 15px rgba(0, 0, 0, 0.1);
  padding: 30px;
  position: relative;
}

h1 {
  font-family: 'Georgia', serif;
  color: #4b2e83;
  font-size: 3rem;
  text-shadow: 2px 2px 5px rgba(0, 0, 0, 0.2);
}

button {
  font-size: 1rem;
  border-radius: 5px;
}

button:hover {
  background-color: #6a1b9a;
}

.note-list {
  margin-top: 30px;
}

/* Добавим декоративную обводку */
.container::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  border: 15px solid #7e57c2;
  border-radius: 15px;
  box-shadow: inset 0 0 20px rgba(0, 0, 0, 0.2);
}
</style>
