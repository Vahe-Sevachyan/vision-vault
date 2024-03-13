<template>
  <div class="card" :style="{ backgroundColor: note.backgroundColor }">
    <div class="card-title-container">
      <p>Card Header</p>
      <ul class="editBtn-container">
        <li @click="editNoteHandler(note)">
          <img src="../assets/edit.svg" alt="" />
        </li>
        <li @click="deleteCard">
          <img src="../assets/trash.svg" alt="" />
        </li>
      </ul>
    </div>
    <div class="text-container">
      <p class="main-text">{{ note.text }}</p>
    </div>
    <p class="date">{{ note.date.toLocaleString("en-US") }}</p>
  </div>
</template>

<script setup>
import { defineProps, emit } from "vue";

const { note } = defineProps(["note"]);

const editNoteHandler = () => {
  emit("editNoteHandler", note);
};

const deleteCard = () => {
  emit("deleteCard");
};
</script>
