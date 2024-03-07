<script setup>
import { ref } from "vue";
const showModal = ref(false);
const newNote = ref("");
const notes = ref([]);
const errorMessage = ref("");
function toggleModal() {
  showModal.value = true;
}
function closeModal() {
  showModal.value = false;
}

function getRandomColor() {
  return "hsl(" + Math.random() * 360 + ", 100%, 75%)";
}
const addNote = () => {
  if (newNote.value.length < 10) {
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
</script>

<template>
  <main>
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
    <div class="container">
      <header>
        <h1>Vision Vault</h1>
        <button v-on:click="toggleModal()">Create Note</button>
      </header>
      <div class="cards-container">
        <div
          v-for="note in notes"
          v-bind:key="note.id"
          class="card"
          v-bind:style="{ backgroundColor: note.backgroundColor }"
        >
          <p class="main-text">{{ note.text }}</p>
          <p class="date">{{ note.date.toLocaleString("en-US") }}</p>
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped>
main {
  height: 100vh;
  width: 100vw;
}
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
h1 {
  color: white;
  font-family: Tahoma, Geneva, Verdana, sans-serif;
  font-weight: bold;
  margin-bottom: 25px;
  font-size: 35px;
}

.container {
  max-width: 935px;
  padding: 10px;
  margin: 0 auto;
}

header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

/* header button {
  border: none;
  padding: 10px;
  width: 50px;
  height: 50px;
  cursor: pointer;
  background-color: #131730;
  color: white;
  border-radius: 10%;
  font-size: 25px;
  text-align: center;
} */

header button {
  background-image: linear-gradient(
    to right,
    #1a2980 0%,
    #26d0ce 51%,
    #1a2980 100%
  );
  border: none;
  margin: 10px;
  padding: 15px 45px;
  text-align: center;
  text-transform: uppercase;
  transition: 0.5s;
  background-size: 200% auto;
  color: white;
  /* box-shadow: 0 0 0px; */
  border-radius: 10px;
  display: block;
}

header button:hover {
  background-position: right center; /* change the direction of the change here */
  color: #fff;
  text-decoration: none;
  cursor: pointer;
}

.cards-container {
  display: flex;
  flex-wrap: wrap;
  width: 1000px;
}
.card {
  height: 225px;
  min-width: 200px;
  padding: 10px;
  border-radius: 15px;
  flex-direction: column;
  justify-content: space-between;
  margin: 0 20px 20px 0;
}
.main-text {
  margin-bottom: 110px;
}
.modalTitle {
  margin-top: -10px;
  text-align: center;
  font-family: Verdana, Geneva, Tahoma, sans-serif;
  font-size: 20px;
  font-weight: bold;
}
.modal {
  width: 450px;
  background-color: white;
  border-radius: 10px;
  padding: 30px;
  position: relative;
  display: flex;
  flex-direction: column;
}
/* .modal button {
  padding: 10px 20px;
  font-size: 20px;
  width: 100%;
  background-color: blueviolet;
  border: none;
  color: white;
  cursor: pointer;
  margin-top: 15px;
} */

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
  background-color: rgb(197, 14, 14);
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
</style>
