<template>
  <div>App: {{ personName }}</div>
</template>
<script setup>
defineProps({
  personName: {
    type: String,
    required: true,
  },
});
</script>
<style scoped></style>
