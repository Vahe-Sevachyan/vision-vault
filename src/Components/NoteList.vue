<template>
  <div class="cards-container">
    <NoteCard
      v-for="(note, index) in notes"
      :key="note.id"
      :note="note"
      @editNoteHandler="editNoteHandler"
      @deleteCard="deleteCard(index)"
    />
  </div>
</template>

<script setup>
import { defineProps } from "vue";
import NoteCard from "./NoteCard.vue";

const { notes } = defineProps(["notes"]);

const editNoteHandler = (note) => {
  // Logic to edit a note
};

const deleteCard = (index) => {
  // Logic to delete a note
};
</script>
