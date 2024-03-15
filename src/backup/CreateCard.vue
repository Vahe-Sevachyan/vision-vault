<script setup>
import { ref } from "vue";
const showModal = ref(false);
const notes = ref([]);
const newNote = ref("");
const updatedNote = ref("");
const editNote = ref(false);
const selectedNote = ref(null);
const errorMessage = ref("");

function toggleModal() {
  showModal.value = true;
}

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

function saveEdit(note) {
  if (updatedNote.value.length < 5) {
    return (errorMessage.value =
      "Note must be minimum of 10 characters or more!");
  }
  note.text = updatedNote.value;
  editNote.value = false;
}

function closeModal() {
  showModal.value = false;
  newNote.value = "";
  updatedNote.value = null;
}

function editNoteHandler(note) {
  // Open the modal for editing
  editNote.value = true;
  selectedNote.value = note;
  updatedNote.value = note.text;
}

function deleteCard(index) {
  // if (index !== -1) {
  //   notes.value.splice(index, 1);
  // }
  if (index !== -1) {
    notes.value.splice(index, 1);
    // editNote.value.splice(index, 1);
  }
}

function cancelEdit() {
  // Close the modal without saving changes
  editNote.value = false;
}
// function closeModal() {
//   showModal.value = false;
// }
</script>

<template>
  <main>
    <!-- Modal for editing -->
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
        <button v-on:click="addNote()">Save Note</button>
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
          v-for="(note, index) in notes"
          v-bind:key="note.id"
          class="card"
          v-bind:style="{ backgroundColor: note.backgroundColor }"
        >
          <div class="card-title-container">
            <p>Card Header</p>
            <ul class="editBtn-container">
              <li v-on:click="editNoteHandler(note)">
                <img src="../assets/edit.svg" alt="" />
              </li>
              <li v-on:click="deleteCard(index)">
                <img src="../assets/trash.svg" alt="" />
              </li>
            </ul>
          </div>
          <div class="text-container">
            <p class="main-text">{{ note.text }}</p>
          </div>
          <p class="date">{{ note.date.toLocaleString("en-US") }}</p>
        </div>
      </div>
    </div>
  </main>
</template>
<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Barlow+Semi+Condensed:wght@400;600;700&family=Black+Ops+One&family=Kumbh+Sans:wght@400;700&family=Nunito:ital,wght@0,200..1000;1,200..1000&family=Oleo+Script:wght@700&family=Plus+Jakarta+Sans:wght@500;800&family=Poppins:wght@300;400&family=Roboto:wght@400;500&display=swap");

main {
  height: 100vh;
  width: 100vw;
}
.container {
  max-width: 935px;
  padding: 10px;
  margin: 0 auto;
}
/* ***MODAL*** */
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

/* ***HEADER SECTION*** */
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
h1 {
  color: white;
  font-family: "Nunito", Verdana, sans-serif;
  font-weight: bold;
  margin-bottom: 25px;
  font-size: 35px;
}
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
/* ***CARD SECTION*** */
.cards-container {
  display: flex;
  flex-wrap: wrap;
  width: 1000px;
}
.card {
  width: 240px;
  height: 285px;
  padding: 10px;
  border-radius: 15px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  margin: 0 15px 15px 0;
  border: 1px solid white;
}
.text-container {
  width: 210px;
  height: 200px;

  overflow-y: auto;
  border: 1px solid black;
  word-wrap: break-word;
  /* padding: 0; */
  margin-bottom: 7px;
  /* padding-top: none; */
  margin: auto;
  margin-bottom: 10px;
}
.date {
  font-family: "Nunito", Verdana, sans-serif;
  font-size: 13px;
  text-align: center;

  /* height: 5px;
  position: relative;
  top: -6px; */
}
.card-title-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding-top: 5px;
  width: 210px;
  /* height: 30px; */
  border: 1px solid black;
  margin: auto;
}
.card-title-container p {
  margin-bottom: 5px;
}
.card-title-container span {
  font-size: 20px;
}
.editBtn-container {
  display: flex;
  justify-content: space-between;
  /* border: 1px solid black; */
  list-style: none;
}
.editBtn-container img {
  color: white;
  width: 20px;
  cursor: pointer;
}
.editBtn-container img:hover {
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
</style>
