<template>
  <div v-if="editNote" class="overlay">
    <div class="modal">
      <h4 class="modalTitle">Edit Note</h4>
      <textarea
        v-model.trim="updatedNote"
        name="note"
        id="note"
        cols="30"
        rows="10"
      ></textarea>
      <p v-if="errorMessage" class="errorMsg">{{ errorMessage }}</p>
      <button v-on:click="saveEdit(selectedNote)">Save</button>
      <button v-on:click="cancelEdit()" id="close">Cancel</button>
    </div>
  </div>
</template>
<script setup>
import { ref } from "vue";
function saveEdit(note) {
  if (updatedNote.value.length < 5) {
    return (errorMessage.value =
      "Note must be minimum of 10 characters or more!");
  }
  note.text = updatedNote.value;
  editNote.value = false;
}
function cancelEdit() {
  // Close the modal without saving changes
  editNote.value = false;
}
</script>
<style scoped></style>
