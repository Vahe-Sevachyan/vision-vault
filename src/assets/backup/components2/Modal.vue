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
  if (noteText.value.length < 4) {
    errorMessage.value = "Note must be minimum of 4 characters or more!";
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
  // emit("add-note", newNote);
}

function closeModal() {
  noteText.value = "";
  errorMessage.value = "";
}

function getRandomColor() {
  return "hsl(" + Math.random() * 360 + ", 100%, 75%)";
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

.modal button {
  background-image: linear-gradient(
    to right,
    #24c6dc 0%,
    #514a9d 51%,
    #24c6dc 100%
  );
  width: 100%;
  margin-top: 15px;
  padding: 15px 45px;
  text-align: center;
  text-transform: uppercase;
  transition: 0.5s;
  background-size: 200% auto;
  color: white;
  box-shadow: 0 0 20px #eee;
  border-radius: 10px;
  border: none;
  display: block;
}

.modal button:hover {
  background-position: right center; /* change the direction of the change here */
  color: #fff;
  text-decoration: none;
  cursor: pointer;
}

#close {
  background-image: linear-gradient(
    to right,
    #dc2424 0%,
    #4a569d 51%,
    #dc2424 100%
  );
  margin-top: 15px;
  padding: 15px 45px;
  text-align: center;
  text-transform: uppercase;
  transition: 0.5s;
  background-size: 200% auto;
  color: white;
  box-shadow: 0 0 20px #eee;
  border-radius: 10px;
  display: block;
}

#close:hover {
  background-position: right center; /* change the direction of the change here */
  color: #fff;
  text-decoration: none;
}

.errorMsg {
  color: tomato;
  font-family: Verdana, Tahoma, sans-serif;
}

textarea {
  resize: none;
  border: 1.8px solid black;
}
textarea:focus {
  outline: none;
  border: 2px solid #106de6;
}
</style>
