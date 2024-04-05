<template>
  <div>
    <Modal
      v-if="showModal"
      @close="closeModal"
      @add-note="addNote"
      class="modal"
    />
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
          @toggle-card-size="toggleCardSizeHandler(index)"
          @toggle-card-hide="toggleCardHideHandler(index)"
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
const isTextShowing = ref(false);
function toggleModal() {
  showModal.value = true;
}
function toggleCardHideHandler() {
  isTextShowing.value = true;
}
//duplicate this function
function toggleCardSizeHandler() {
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
    selectedNote.value.title = title.replace(/\b\w/g, (char) =>
      char.toUpperCase()
    );
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
.modal {
  display: flex;
}
.note-card {
  margin-bottom: 5px;
}
.container {
  width: 280px;
  max-height: 800px;
  overflow-y: auto;
  overflow-x: hidden;
  /* transition: max-height 5.3s ease-in; */
  transition: max-height 3.25s ease;
  transition-duration: 2s;
  scrollbar-gutter: stable both-edges;
  /* border: 1px solid red; */
  padding-top: 5px;
}

.card-wrapper {
  display: flex;
  flex-direction: column;
  width: 250px;
  justify-content: center;
  align-items: center;
  margin: auto;
  padding-top: 5px;
  padding-bottom: 5px;
  /* border: 1px solid red; */
  /* align-items: center; */
  /* max-height: 800px;
  overflow-y: auto;
  overflow-x: hidden; */
  /* scrollbar-gutter: stable both-edges; */
  /* border: 1px solid red; */
  /* align-items: center; */
  /* flex-wrap: wrap;
  justify-content: flex-start; */
  /* justify-content: flex-start; */
  /* align-items: center; */
}

button {
  background-image: linear-gradient(
    to right,
    #1a2980 0%,
    #26d0ce 51%,
    #1a2980 100%
  );
  font-family: Roboto, sans-serif;
  border: none;
  margin: 10px;
  padding: 10px 35px;
  text-align: center;
  text-transform: uppercase;
  transition: 0.5s;
  background-size: 200% auto;
  color: white;
  /* box-shadow: 0 0 0px; */
  border-radius: 10px;
  display: block;
  margin: auto;
  /* margin: 5px; */
  /* margin: 5px 0 5px 0; */
}

button:hover {
  background-position: right center; /* change the direction of the change here */
  color: #fff;
  text-decoration: none;
  cursor: pointer;
}
</style>
