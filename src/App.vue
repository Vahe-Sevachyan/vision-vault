<template>
  <!-- :note="updatedNote" --3-->
  <main>
    <Modal v-if="showModal" @close="closeModal" @add-note="addNote" />
    <EditModal
      v-if="editNote"
      @close="cancelEditModal"
      @updateNote="saveEdit"
      @updateTitle="saveTitle"
      :modifiedNote="selectedNote.text"
      :modifiedTitle="selectedNote.title"
    />
    <div class="container">
      <header>
        <h1>Vision Vault</h1>
        <button @click="toggleModal()">Create Note</button>
      </header>
      <div class="card-wrapper">
        <NoteCard
          v-for="(note, index) in notes"
          :key="note.id"
          :note="note"
          @edit-note="editNoteHandler(note)"
          @delete-note="deleteNoteHandler(index)"
        />
      </div>
    </div>
  </main>
</template>

<script setup>
import { ref } from "vue";
import Modal from "./components/Modal.vue";
import NoteCard from "./components/NoteCard.vue";
import EditModal from "./components/EditModal.vue";
const showModal = ref(false);
const notes = ref([]);
const selectedNote = ref(null);
// const selectedTitle = ref(null);
const editNote = ref(false);
// const updatedNote = ref("");
function toggleModal() {
  showModal.value = true;
}

function addNote(newNote) {
  notes.value.push(newNote);
  showModal.value = false;
}

function editNoteHandler(note) {
  // Open the modal for editing
  editNote.value = true;
  selectedNote.value = note;
  // selectedTitle.value = note;
}
function saveTitle(updatedTitle) {
  if (selectedNote.value) {
    selectedNote.value.title = updatedTitle;
  }
}
function saveEdit(updatedNote) {
  if (selectedNote.value) {
    selectedNote.value.text = updatedNote;
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
// function editNoteHandler(note) {
//   showModal.value = true;
//   // Handle edit note logic
// }
</script>

<style scoped>
main {
  height: 100vh;
  width: 100vw;
}
.container {
  max-width: 1700px;
  padding: 10px;
  margin: 0 auto;
}
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  max-width: 800px;
  margin: 0 auto;
}
.card-wrapper {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  /* justify-content: flex-start; */
  /* border: 1px solid red; */
  align-items: center;
}
h1 {
  color: white;
  font-family: "Nunito", Verdana, sans-serif;
  font-weight: bold;
  margin-bottom: 25px;
  font-size: 35px;
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
