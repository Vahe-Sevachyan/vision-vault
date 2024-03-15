<template>
  <div class="overlay">
    <div class="modal">
      <p class="modalTitle">{{ title }}</p>
      <textarea
        v-model.trim="noteText"
        name="note"
        id="note"
        cols="30"
        rows="10"
        :placeholder="placeholder"
      ></textarea>
      <p v-if="errorMessage" class="errorMsg">{{ errorMessage }}</p>
      <button @click="saveNote">{{ saveButtonText }}</button>
      <button id="close" @click="closeModal">{{ closeButtonText }}</button>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

const noteText = ref("");
const errorMessage = ref("");

const title = ref("New Note");
const placeholder = ref("Enter note...");
const saveButtonText = ref("Save Note");
const closeButtonText = ref("Close");

function saveNote() {
  if (noteText.value.length < 10) {
    errorMessage.value = "Note must be minimum of 10 characters or more!";
    return;
  }
  const newNote = {
    id: Math.floor(Math.random() * 10000000),
    text: noteText.value,
    date: new Date(),
    backgroundColor: getRandomColor(),
  };
  errorMessage.value = "";
  noteText.value = "";
  $emit("add-note", newNote);
}

function closeModal() {
  noteText.value = "";
  errorMessage.value = "";
  $emit("close");
}

function getRandomColor() {
  return "hsl(" + Math.random() * 360 + ", 100%, 75%)";
}
</script>

<style scoped>
/* Styles for Modal.vue */
</style>
