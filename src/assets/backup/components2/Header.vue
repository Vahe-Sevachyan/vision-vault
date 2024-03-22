<template>
  <header>
    <h1>Vision Vault</h1>
    <button @click="toggleModal()">Create Note</button>
  </header>
</template>
<script setup>
// import { defineProps } from "vue";
import { ref, defineProps } from "vue";
const showModal = defineProps().showModal;
// function toggleModal() {
//   showModal.value = true;
// }

defineProps({
  quiz: {
    type: Object,
    required: true,
  },
});
</script>
<style scoped>
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
</style>
