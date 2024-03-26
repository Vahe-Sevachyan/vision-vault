<template>
  <div class="card" :style="{ backgroundColor: note.backgroundColor }">
    <div class="card-title-container">
      <p>Card Header</p>
      <ul class="editBtn-container">
        <li @click="editNote"><img src="../assets/edit.svg" alt="" /></li>
        <li @click="deleteNote"><img src="../assets/trash.svg" alt="" /></li>
      </ul>
    </div>
    <!--No styles for text-container -->
    <div class="text-container">
      <p class="main-text">{{ note.text }}</p>
    </div>
    <p class="date">{{ note.date.toLocaleString("en-US") }}</p>
  </div>
</template>

<script setup>
import { ref, defineProps } from "vue";
const emit = defineEmits("edit-note", "delete-note");
const props = defineProps({
  note: Object,
});
const note = ref(props.note);

function editNote() {
  emit("edit-note", note.value);
}

function deleteNote() {
  emit("delete-note", note.value);
}
</script>

<style scoped>
/* .cards-container {
  display: flex;
  flex-wrap: wrap;
  width: 1000px;
} */
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
</style>
