<template>
  <div>
    <!-- Button to add new note -->
    <button @click="toggleModal(null)">Add Note</button>

    <!-- Modal for editing note -->
    <div v-if="showModal" class="modal">
      <div class="modal-content">
        <textarea v-model="editedNote"></textarea>
        <button @click="saveEdit">Save</button>
        <button @click="cancelEdit">Cancel</button>
      </div>
    </div>

    <!-- Display existing notes -->
    <div v-for="(note, index) in notes" :key="index" class="note">
      <p>{{ note }}</p>
      <button @click="toggleModal(index)">Edit</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      notes: [],
      showModal: false,
      editedNote: "",
      editedIndex: null,
    };
  },
  methods: {
    // Toggle modal for editing note
    toggleModal(index) {
      this.editedIndex = index;
      if (index !== null) {
        this.editedNote = this.notes[index];
      } else {
        this.editedNote = "";
      }
      this.showModal = true;
    },
    // Save edited note
    saveEdit() {
      if (this.editedIndex !== null) {
        this.notes[this.editedIndex] = this.editedNote;
      } else {
        this.notes.push(this.editedNote);
      }
      this.closeModal();
    },
    // Close modal without saving changes
    cancelEdit() {
      this.closeModal();
    },
    // Close modal
    closeModal() {
      this.showModal = false;
      this.editedNote = "";
      this.editedIndex = null;
    },
  },
};
</script>

<style>
.modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal-content {
  background-color: white;
  padding: 20px;
  border-radius: 5px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.5);
}

.note {
  margin-bottom: 10px;
}

button {
  margin-left: 5px;
}
</style>
