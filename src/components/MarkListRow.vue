<script setup>
const props = defineProps(['marks'])

// Emit event in the parent component
const emit = defineEmits(['onRemoveClicked'])
function emitRemoveClicked(mark) {
  emit('onRemoveClicked', mark)
}
</script>

<template>
  <tr class="mark-table-row" v-for="mark in props.marks" :key="mark.id">
    <td>{{ mark.date }}</td>
    <td>{{ mark.course.charAt(0).toUpperCase() + mark.course.slice(1) }}</td>
    <td>{{ mark.professor }}</td>
    <td>{{ mark.mark }}</td>
    <td><button @click="emitRemoveClicked(mark)">X</button></td>
  </tr>
</template>

<style scoped>
.mark-table-row {
  border-bottom: 1px solid #000;
  padding: 0.5rem;
}
.mark-table-row:nth-child(even) {
  background-color: #f0f0f0;
}

.mark-table-row:nth-child(odd) {
  background-color: #ffffff;
}
</style>
