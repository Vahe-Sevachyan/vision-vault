<template>
  <div
    :class="['card', { expanded: isCardExpanded }]"
    :style="{ backgroundColor: note.backgroundColor }"
  >
    <div class="card-title-container">
      <p>{{ note.title }}</p>
      <ul class="editBtn-container">
        <li @click="editNote"><img src="../assets/edit.svg" alt="" /></li>
        <li @click="deleteNote"><img src="../assets/trash.svg" alt="" /></li>
      </ul>
    </div>
    <!--No styles for text-container -->
    <div class="text-container">
      <p class="main-text">{{ note.text }}</p>
    </div>
    <button
      class="toggle-button"
      @click="toggleCard"
      :style="{ backgroundColor: note.btnColor }"
    >
      <span v-if="!isCardExpanded">
        <img src="../assets/arrow-down.svg" alt=""
      /></span>
      <span v-else> <img src="../assets/arrow-up.svg" alt="" /></span>
      <!-- Toggle -->
    </button>
    <p class="date">{{ note.date.toLocaleString("en-US") }}</p>
  </div>
</template>

<script setup>
import { ref, defineProps } from "vue";
const emit = defineEmits("edit-note", "delete-note");
const isCardExpanded = ref(false);
const props = defineProps({
  note: Object,
});
const note = ref(props.note);

function toggleCard() {
  isCardExpanded.value = !isCardExpanded.value;
  emit("toggle-card", isCardExpanded.value);
}

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

.toggle-button {
  width: 30%;
  /* height: 70px; */
  /* padding: 16px; */
  border-radius: 15px;
  border: none;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  margin-bottom: 15px;
  margin: auto;
  cursor: pointer;
}
span {
  display: flex;
  align-items: center;
  justify-content: center;
}
.card {
  width: 240px;
  height: 185px;
  padding: 10px;
  border-radius: 15px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  margin: 15px 15px 15px 0;
  margin: auto;
  /* border: 1px solid white; */
  overflow: hidden;
  transition: height 4.3s ease-in-out;
}

.card.expanded {
  height: auto;
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
  height: 300px;
  /* overflow-y: auto; */
  border: 1px solid black;
  word-wrap: break-word;
  margin-bottom: 7px;
  margin: auto;
  margin-bottom: 10px;
  overflow: hidden;
}
.date {
  font-family: "Nunito", Verdana, sans-serif;
  font-size: 13px;
  text-align: center;
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
