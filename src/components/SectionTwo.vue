<template>
  <div>
    <Modal v-if="showModal" @close="closeModal" @add-note="addNote" />
    <EditModal
      v-if="editNote"
      @close="cancelEditModal"
      @updateNote="saveEdit"
      :modifiedNote="selectedNote.text"
      :modifiedTitle="selectedNote.title"
    />
    <!-- @updateTitle="saveTitle" -->
    <div class="container">
      <button @click="toggleModal()">Create Note</button>

      <div class="card-wrapper">
        <NoteCard
          v-for="(note, index) in notes"
          :key="note.id"
          :note="note"
          @edit-note="editNoteHandler(note)"
          @delete-note="deleteNoteHandler(index)"
          @toggle-card="toggleCardHandler(index)"
          class="note-card"
        />
      </div>
    </div>
  </div>
</template>
<script setup>
import { ref } from "vue";
import Modal from "./Modal.vue";
import NoteCard from "./NoteCard.vue";
import EditModal from "./EditModal.vue";
const showModal = ref(false);
const notes = ref([]);
const selectedNote = ref(null);
const editNote = ref(false);
// const selectedTitle = ref(null);
// const updatedNote = ref("");
const isCardExpanded = ref(false);
function toggleModal() {
  showModal.value = true;
}

//duplicate this function
function toggleCardHandler() {
  isCardExpanded.value = true;
}

function addNote(newNote) {
  notes.value.push(newNote);
  showModal.value = false;
}

function editNoteHandler(note) {
  // Open the modal for editing
  editNote.value = true;
  selectedNote.value = note;
}

function saveEdit({ note, title }) {
  if (selectedNote.value) {
    selectedNote.value.text = note;
    selectedNote.value.title = title;
    editNote.value = false;
    selectedNote.value = null;
  }
}

function closeModal() {
  showModal.value = false;
}

function cancelEditModal() {
  editNote.value = false;
  selectedNote.value = null;
}

function deleteNoteHandler(index) {
  if (index !== -1) {
    notes.value.splice(index, 1);
    // editNote.value.splice(index, 1);
  }
  // notes.value.splice(index, 1);
}
</script>

<style scoped>
.container {
  max-width: 330px;
  padding: 10px;
  /* margin: 0 auto; */
  border: 1px solid red;
  max-height: 800px;
  overflow-y: auto;
  overflow-x: hidden;
}
.note-card {
  margin: auto;
  margin-bottom: 5px;
}
.card-wrapper {
  display: flex;
  flex-direction: column;
  /* justify-content: flex-start; */
  border: 1px solid red;
  /* align-items: center; */
}

header button {
  background-image: linear-gradient(
    to right,
    #1a2980 0%,
    #26d0ce 51%,
    #1a2980 100%
  );
  border: none;
  margin: 10px;
  padding: 15px 45px;
  text-align: center;
  text-transform: uppercase;
  transition: 0.5s;
  background-size: 200% auto;
  color: white;
  /* box-shadow: 0 0 0px; */
  border-radius: 10px;
  display: block;
}

header button:hover {
  background-position: right center; /* change the direction of the change here */
  color: #fff;
  text-decoration: none;
  cursor: pointer;
}
</style>
