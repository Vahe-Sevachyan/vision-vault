<template lang="">
  <div class="container">
    <header>
      <h1>Vision Vault</h1>
      <button v-on:click="toggleModal()">Create Note</button>
    </header>
    <div class="cards-container">
      <div
        v-for="(note, index) in notes"
        v-bind:key="note.id"
        class="card"
        v-bind:style="{ backgroundColor: note.backgroundColor }"
      >
        <div class="card-title-container">
          <p>Card Header</p>
          <ul class="editBtn-container">
            <li v-on:click="editNoteHandler(note)">
              <img src="../assets/edit.svg" alt="" />
            </li>
            <li v-on:click="deleteCard(index)">
              <img src="../assets/trash.svg" alt="" />
            </li>
          </ul>
        </div>
        <div class="text-container">
          <p class="main-text">{{ note.text }}</p>
        </div>
        <p class="date">{{ note.date.toLocaleString("en-US") }}</p>
      </div>
    </div>
  </div>
</template>
<script setup>
import { ref } from "vue";
function toggleModal() {
  showModal.value = true;
}
function deleteCard(index) {
  // if (index !== -1) {
  //   notes.value.splice(index, 1);
  // }
  if (index !== -1) {
    notes.value.splice(index, 1);
    editNote.value.splice(index, 1); // Remove corresponding entry from editNote array
  }
}
function editNoteHandler(note) {
  // Open the modal for editing
  // editNote.value = true;
  // updatedNote.value = note.text;
  editNote.value = true;
  selectedNote.value = note;
  updatedNote.value = note.text;
}
</script>
<style scoped></style>
