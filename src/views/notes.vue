<template>
  <main class="notes-app">
  
    <section class="create-note">
      <h3>CREATE A NOTE</h3>

      <form id="new-note-form" @submit.prevent="addNote">
        <h4>What's on your mind?</h4>
        <input
          type="text"
          name="content"
          id="content"
          placeholder="Enter your note"
          v-model="input_content"
        />

        <h4>Pick a category</h4>
        <div class="options">
          <label>
            <input
              type="radio"
              name="category"
              id="category1"
              value="personal"
              v-model="input_category"
            />
            <span class="bubble personal"></span>
            <div>Personal</div>
          </label>

          <label>
            <input
              type="radio"
              name="category"
              id="category2"
              value="work"
              v-model="input_category"
            />
            <span class="bubble work"></span>
            <div>Work</div>
          </label>
        </div>

        <input type="submit" value="Add note" />
      </form>
    </section>

    <section class="note-list">
      <h3>NOTE LIST</h3>
      <div class="list" id="note-list">
        <div v-for="note in notes_asc" :key="note.id" :class="`note-item ${note.done && 'done'}`">
          
          <div class="note-content">
            <input type="text" v-model="note.content" />
          </div>

          <div class="actions">
            <button class="delete" @click="removeNote(note)">Delete</button>
          </div>
        </div>
      </div>
    </section>
  </main>
</template>

<script>
import { ref, computed } from 'vue';

export default {
  name: 'notesApp',
  components: {},
  setup() {
    const notes = ref([]);
    const name = ref('');
    const input_content = ref('');
    const input_category = ref(null);

    const notes_asc = computed(() => {
      return [...notes.value].sort((a, b) => a.createdAt - b.createdAt);
    });

    const addNote = () => {
      if (input_content.value.trim() === '' || input_category.value === null) {
        return;
      }

      const newNote = {
        content: input_content.value,
        category: input_category.value,
        done: false,
        editable: false,
        createdAt: new Date().getTime(),
      };

      notes.value.push(newNote);
    };

    const removeNote = (note) => {
      notes.value = notes.value.filter((n) => n !== note);
    };

    return {
      name,
      input_content,
      input_category,
      notes,
      notes_asc,
      addNote,
      removeNote,
    };
  },
};
</script>
