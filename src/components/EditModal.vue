<template>
  <div class="overlay">
    <div class="modal">
      <h4 class="modalTitle">Edit Note</h4>
      <div>
        <input
          type="text"
          class="title-input"
          v-model.trim="updatedTitle"
          ref="titleInput"
        />
      </div>
      <textarea
        ref="editTextarea"
        v-model.trim="updatedNote"
        name="note"
        id="note"
        cols="30"
        rows="10"
      ></textarea>
      <p v-if="errorMessage" class="errorMsg">{{ errorMessage }}</p>
      <button v-on:click="saveEdit()">Save Note</button>
      <button v-on:click="cancelEditModal()" id="close">Cancel</button>
    </div>
  </div>
</template>
<script setup>
// import { ref, defineEmits } from "vue"; --1
import { ref, defineProps, defineEmits } from "vue";
const emit = defineEmits(["close", "updateNote", "updateTitle"]);

const props = defineProps({
  modifiedNote: {
    type: String,
    required: true,
  },
  modifiedTitle: {
    type: String,
    required: true,
  },
});

function cancelEditModal() {
  updatedNote.value = "";
  updatedTitle.value = "";
  emit("close");
  //   errorMessage.value = "";
}

function saveEdit() {
  //   emit("updateNote", updatedNote.value);
  //   emit("updateTitle", updatedTitle.value);
  emit("updateNote", updatedNote.value);
  emit("updateTitle", updatedTitle.value);
}

const updatedNote = ref(props.modifiedNote);
const updatedTitle = ref(props.modifiedTitle);
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
.title-input {
  border: 1px solid black;
  margin-bottom: 10px;
  width: 100%;
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
