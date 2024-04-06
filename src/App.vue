<template>
  <main>
    <header>
      <h1>Vision Vault</h1>
    </header>
    <div class="container">
      <SectionOne />
      <SectionTwo />
      <SectionThree />
      <SectionFour />
      <!-- <SectionFive />
      <SectionSix /> -->
    </div>
  </main>
  <link
    rel="stylesheet"
    href="https://pro.fontawesome.com/releases/v5.10.0/css/all.css"
    integrity="sha384-AYmEC3Yw5cVb3ZcuHtOA93w35dYTsvhLPVnYs9eStHfGJvOvKxVfELGroGkvsg+p"
    crossorigin="anonymous"
  />
</template>

<script setup>
import SectionOne from "./components/SectionOne.vue";
import SectionTwo from "./components/SectionTwo.vue";
import SectionThree from "./components/SectionThree.vue";
import SectionFour from "./components/SectionFour.vue";
</script>

<style scoped>
.container {
  max-width: 1200px;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  margin: auto;
}
main {
  height: 100vh;
  width: 100vw;
}
header {
  display: flex;
  justify-content: center;
  align-items: center;
  max-width: 800px;
  margin: 0 auto;
}

h1 {
  color: white;
  font-family: "Poppins", Verdana, sans-serif;
  font-weight: bold;
  font-weight: 400;
  margin-bottom: 25px;
  margin-top: 15px;
  font-size: 45px;
}
@media only screen and (max-width: 1125px) {
  .container {
    max-width: 560px;
  }
}
@media only screen and (max-width: 560px) {
  .container {
    max-width: 330px;
    justify-content: center;
    margin: auto;
  }
}
</style>
// function editNoteHandler(note) { // showModal.value = true; // // Handle edit
note logic // } // function saveEdit(updatedNote) { // if (selectedNote.value) {
// selectedNote.value.text = updatedNote; // editNote.value = false; //
selectedNote.value = null; // } // } // function saveTitle(updatedTitle) { // if
(selectedNote.value) { // selectedNote.value.title = updatedTitle; //
console.log(selectedNote.value.title); // } // }
