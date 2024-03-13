<script setup>
import { ref } from "vue";

const newNote = ref("");
const updatedNote = ref("");
const editNote = ref(false);
const selectedNote = ref(null);

// function closeModal() {
//   showModal.value = false;
// }
</script>

<template></template>
<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Barlow+Semi+Condensed:wght@400;600;700&family=Black+Ops+One&family=Kumbh+Sans:wght@400;700&family=Nunito:ital,wght@0,200..1000;1,200..1000&family=Oleo+Script:wght@700&family=Plus+Jakarta+Sans:wght@500;800&family=Poppins:wght@300;400&family=Roboto:wght@400;500&display=swap");

/*             ***MODAL***          */

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
