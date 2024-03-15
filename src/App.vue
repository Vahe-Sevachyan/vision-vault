<template>
  <main>
    <Modal v-if="showModal" @close="closeModal" @add-note="addNote" />
    <div class="container">
      <header>
        <h1>Vision Vault</h1>
        <button @click="toggleModal()">Create Note</button>
      </header>
      <NoteCard
        v-for="(note, index) in notes"
        :key="note.id"
        :note="note"
        @edit-note="editNoteHandler"
        @delete-note="deleteCard(index)"
      />
    </div>
  </main>
</template>

<script setup>
import { ref } from "vue";
import Modal from "./components/Modal.vue";
import NoteCard from "./components/NoteCard.vue";

const showModal = ref(false);
const notes = ref([]);

function toggleModal() {
  showModal.value = true;
}

function addNote(newNote) {
  notes.value.push(newNote);
  showModal.value = false;
}

function closeModal() {
  showModal.value = false;
}

function editNoteHandler(note) {
  showModal.value = true;
  // Handle edit note logic
}

function deleteCard(index) {
  notes.value.splice(index, 1);
}
</script>

<style scoped>
main {
  height: 100vh;
  width: 100vw;
}
.container {
  max-width: 935px;
  padding: 10px;
  margin: 0 auto;
}
header {
  display: flex;
  justify-content: space-between;
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
