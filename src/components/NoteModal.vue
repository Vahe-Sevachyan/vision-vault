<template>
  <div v-if="visible" class="overlay">
    <div class="modal">
      <h4 class="modalTitle">{{ title }}</h4>
      <textarea
        v-model.trim="noteText"
        name="note"
        id="note"
        cols="30"
        rows="10"
      ></textarea>
      <p v-if="errorMessage" class="errorMsg">{{ errorMessage }}</p>
      <button v-if="isEdit" @click="saveEdit">Save</button>
      <button v-else @click="addNote">Add Note</button>
      <button @click="cancel">Cancel</button>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

const visible = ref(false);
const noteText = ref("");
const errorMessage = ref("");
const isEdit = ref(false);
const title = ref("New Note");

function toggleModal() {
  visible.value = true;
  noteText.value = "";
  errorMessage.value = "";
  isEdit.value = false;
  title.value = "New Note";
}

function openEditModal(note) {
  visible.value = true;
  noteText.value = note.text;
  isEdit.value = true;
  title.value = "Edit Note";
}

function addNote() {
  // Add note logic
}

function saveEdit() {
  // Save edited note logic
}

function cancel() {
  visible.value = false;
}
</script>
