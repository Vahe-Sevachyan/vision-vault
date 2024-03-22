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

/* ***MODAL*** */

/* ***HEADER SECTION*** */

/* ***CARD SECTION*** */

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
