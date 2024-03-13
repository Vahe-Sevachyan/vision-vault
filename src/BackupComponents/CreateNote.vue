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
const showModal = ref(false);
const errorMessage = ref("");
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
<style scoped>
.overlay {
  position: absolute;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.77);
  z-index: 10px;
  display: flex;
  align-items: center;
  justify-content: center;
}
.modalTitle {
  margin-top: -15px;
  margin-bottom: 15px;
  text-align: center;
  font-family: "Nunito", Verdana, sans-serif;
  font-size: 25px;
  font-weight: bold;
}
.modal {
  width: 450px;
  background-color: #ffffff;
  border-radius: 10px;
  padding: 30px;
  position: relative;
  display: flex;
  flex-direction: column;
}

.errorMsg {
  color: tomato;
  font-family: Verdana, Tahoma, sans-serif;
}
</style>
