<template>
  <div v-if="showModal" class="overlay">
    <div class="modal">
      <h4 class="modalTitle">{{ title }}</h4>
      <textarea
        v-model.trim="newNote"
        name="note"
        id="note"
        cols="30"
        rows="10"
      ></textarea>
      <p v-if="errorMessage" class="errorMsg">{{ errorMessage }}</p>
      <button @click="addNote">{{ buttonText }}</button>
      <button @click="closeModal" id="close">Close</button>
    </div>
  </div>
</template>

<script setup>
import { defineProps, ref } from "vue";

const { showModal, newNote, errorMessage } = defineProps([
  "showModal",
  "newNote",
  "errorMessage",
]);

const addNote = () => {
  // Logic to add a new note
};

const closeModal = () => {
  // Logic to close the modal
};

const title = ref("New Note");
const buttonText = ref("Add Note");
</script>
