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

<script setup>
import { ref } from "vue";

const notes = ref([]);
const showModal = ref(false);
const editedNote = ref("");
const editedIndex = ref(null);

// Toggle modal for editing note
const toggleModal = (index) => {
  editedIndex.value = index;
  if (index !== null) {
    editedNote.value = notes.value[index];
  } else {
    editedNote.value = "";
  }
  showModal.value = true;
};

// Save edited note
const saveEdit = () => {
  if (editedIndex.value !== null) {
    notes.value[editedIndex.value] = editedNote.value;
  } else {
    notes.value.push(editedNote.value);
  }
  closeModal();
};

// Close modal without saving changes
const cancelEdit = () => {
  closeModal();
};

// Close modal
const closeModal = () => {
  showModal.value = false;
  editedNote.value = "";
  editedIndex.value = null;
};
</script>

<style scoped>
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
