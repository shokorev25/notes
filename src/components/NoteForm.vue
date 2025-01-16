<template>
  <div class="note-form card p-4 mb-4 shadow-sm">
    <h5 class="card-title">Новая заметка</h5>
    <input
      v-model="noteTitle"
      type="text"
      class="form-control mb-3"
      placeholder="Заголовок"
    />
    <textarea
      v-model="noteText"
      class="form-control mb-3"
      rows="4"
      placeholder="Содержание заметки"
    ></textarea>
    <button @click="addNote" class="btn btn-primary add-btn">Добавить заметку</button>
  </div>
</template>

<script>
export default {
  name: 'NoteForm',
  data() {
    return {
      noteTitle: '',
      noteText: '',
    };
  },
  methods: {
    addNote() {
      if (this.noteTitle.trim() && this.noteText.trim()) {
        const currentDate = new Date().toLocaleString();
        this.$emit('add-note', {
          id: Date.now(),
          title: this.noteTitle,
          text: this.noteText,
          date: currentDate,
        });
        this.noteTitle = '';
        this.noteText = '';
      }
    },
  },
};
</script>

<style scoped>
.note-form {
  background-color: #fff5e6;
  border-radius: 12px;
  border: 1px solid #d1b7b1;
  box-shadow: inset 0 0 15px rgba(0, 0, 0, 0.1);
}

textarea,
input {
  font-family: 'Courier New', Courier, monospace;
  background-color: #f5f5f5;
}

input::placeholder,
textarea::placeholder {
  font-style: italic;
  color: #8c8c8c;
}

.add-btn {
  font-weight: bold;
  background-color: #7e57c2;
  color: white;
  border-radius: 8px;
}

.add-btn:hover {
  background-color: #5e35b1;
}
</style>
