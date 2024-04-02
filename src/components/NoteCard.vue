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
  border-radius: 5px;
  border: none;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  margin: auto;
  cursor: pointer;
  margin-bottom: 4.5px;
}
span {
  display: flex;
  align-items: center;
  justify-content: center;
}
.card {
  width: 230px;
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
  margin: 4px 0 4px 0;
}

.card.expanded {
  height: auto;
}
.card-title-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding-top: 5px;
  width: 200px;
  font-size: 19px;
  font-family: Tahoma, Geneva, sans-serif;
  letter-spacing: 1px;
  /* height: 30px; */
  /* border: 1px solid black; */
  margin: auto;
  margin-bottom: 5px;
}

.text-container {
  font-family: Verdana, Geneva, Tahoma, sans-serif;
  width: 210px;
  height: 300px;
  letter-spacing: 0.3px;
  /* overflow-y: auto; */
  border: 2px solid black;
  word-wrap: break-word;
  margin-bottom: 7px;
  margin: auto;
  margin-bottom: 8px;
  overflow: hidden;
  border-radius: 10px;
  padding: 3px;
  font-size: 14px;
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
