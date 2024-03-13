<template>
  <div id="app">
    <Header @toggleModal="toggleModal" />
    <NoteModal
      :showModal="showModal"
      @addNote="addNote"
      @closeModal="closeModal"
      :errorMessage="errorMessage"
      :newNote="newNote"
    />
    <NoteList
      :notes="notes"
      @editNoteHandler="editNoteHandler"
      @deleteCard="deleteCard"
    />
  </div>
</template>

<script setup>
import { ref } from "vue";
import Header from "./components/Header.vue";
import NoteModal from "./components/NoteModal.vue";
import NoteList from "./components/NoteList.vue";

const showModal = ref(false);
const notes = ref([]);
const newNote = ref("");
const errorMessage = ref("");

function toggleModal() {
  showModal.value = true;
}

// Other functions and data...
</script>
