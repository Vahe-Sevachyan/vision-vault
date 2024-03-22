<template>
  <main>
    <Modal v-if="showModal" @close="closeModal" @add-note="addNote" />
    <div class="container">
      <Header :showModal="showModal" />
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
import Header from "./components/Header.vue";

const showModal = ref(false);
const notes = ref([]);

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
</style>
