<template>
  <div class="card" :style="{ backgroundColor: note.backgroundColor }">
    <div class="card-title-container">
      <p>Card Header</p>
      <ul class="editBtn-container">
        <li @click="editNote"><img src="../assets/edit.svg" alt="" /></li>
        <li @click="deleteNote"><img src="../assets/trash.svg" alt="" /></li>
      </ul>
    </div>
    <div class="text-container">
      <p class="main-text">{{ note.text }}</p>
    </div>
    <p class="date">{{ note.date.toLocaleString("en-US") }}</p>
  </div>
</template>

<script setup>
import { ref } from "vue";

const note = ref(props.note);

function editNote() {
  $emit("edit-note", note.value);
}

function deleteNote() {
  $emit("delete-note", note.value);
}
</script>

<style scoped>
/* Styles for NoteCard.vue */
</style>
