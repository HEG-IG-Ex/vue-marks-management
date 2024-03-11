<script setup>
const props = defineProps(['courses'])

// Emit event in the parent component
const emit = defineEmits(['onCourseSelected'])

function emitCourseSelected(e) {
  emit('onCourseSelected', e.target.value)
}
</script>

<template>
  <label for="course" class="filter-label">Category</label>
  <select id="course" class="filter-item" @change="emitCourseSelected">
    <option v-for="(course, idx) in props.courses" :key="idx" :value="course.toLowerCase()">
      {{ course }}
    </option>
  </select>
</template>

<style scoped>
.filter-item {
  display: flex;
  flex-direction: column;
}
.filter-label {
  margin-bottom: 5px;
  color: var(--color-secondary);
  font-weight: bold;
}
</style>
