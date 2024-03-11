<template>
  <table class="mark-table">
    <thead>
      <th>Date</th>
      <th>Subject</th>
      <th>Mark</th>
      <th>Action</th>
    </thead>
    <tbody>
      <tr class="mark-table-row" v-for="mark in marks" :key="mark.id">
        <td>{{ mark.date }}</td>
        <td>{{ mark.subject }}</td>
        <td>{{ mark.mark }}</td>
        <td><button>X</button></td>
      </tr>
    </tbody>
  </table>
</template>

<script setup>
import { ref, reactive, computed, watch } from 'vue'
const marks = ref([
  { id: 1, date: '2021-10-01', subject: 'Math', mark: 90 },
  { id: 2, date: '2021-10-01', subject: 'Science', mark: 85 },
  { id: 3, date: '2021-10-01', subject: 'English', mark: 95 },
  { id: 4, date: '2021-10-01', subject: 'History', mark: 80 },
  { id: 5, date: '2021-10-01', subject: 'Geography', mark: 75 }
])
// Your component logic here
</script>

<style scoped>
/* Your component styles here */
.mark-table {
  width: 100%;
  border-collapse: collapse;
}
.mark-table th,
.mark-table td {
  border-bottom: 1px solid #000;
  padding: 0.5rem;
}
.mark-table th {
  background-color: #f0f0f0;
}
.mark-table-row:nth-child(even) {
  background-color: #f0f0f0;
}

.mark-table-row:nth-child(odd) {
  background-color: #ffffff;
}
.mark-table th {
  text-align: left;
  font-weight: bold;
  background-color: var(--color-primary);
  color: #ffffff;
}
</style>
