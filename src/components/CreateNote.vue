<template>
  <div v-if="showModal" class="overlay">
    <div class="modal">
      <p class="modalTitle">New Note</p>
      <textarea
        v-model.trim="newNote"
        name="note"
        id="note"
        cols="30"
        rows="10"
        placeholder="Enter note..."
      ></textarea>
      <p v-if="errorMessage" class="errorMsg">{{ errorMessage }}</p>
      <button v-on:click="addNote()">Add Note</button>
      <button id="close" v-on:click="closeModal()">Close</button>
    </div>
  </div>
</template>
<script setup>
import { ref } from "vue";

function getRandomColor() {
  return "hsl(" + Math.random() * 360 + ", 100%, 75%)";
}
const addNote = () => {
  if (newNote.value.length < 5) {
    return (errorMessage.value =
      "Note must be minimum of 10 characters or more!");
  }
  notes.value.push({
    id: Math.floor(Math.random() * 10000000),
    text: newNote.value,
    date: new Date(),
    backgroundColor: getRandomColor(),
  });
  showModal.value = false;
  newNote.value = "";
  errorMessage.value = "";
};
function closeModal() {
  showModal.value = false;
  newNote.value = "";
  updatedNote.value = null;
}
</script>
<style scoped></style>
