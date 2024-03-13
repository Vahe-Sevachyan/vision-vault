<template>
  <header>
    <h1>Vision Vault</h1>
    <button @click="toggleModal">Create Note</button>
  </header>
</template>
<script setup>
import { defineProps, emit } from "vue";

const { toggleModal } = defineProps(["toggleModal"]);
</script>
<style scoped></style>
