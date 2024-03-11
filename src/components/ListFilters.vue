<script setup>
import CourseSelect from './CourseSelect.vue'

const courses = ['All', 'Math', 'Science', 'English', 'History', 'Geography']

// Emit event in the parent component
const emit = defineEmits(['onSearchChanged', 'onCourseSelected'])

function emitCourseSelected(course) {
  emit('onCourseSelected', course)
}
function emitSearchChanged(e) {
  emit('onSearchChanged', e.target.value)
}
</script>

<template>
  <div class="filter-wrapper">
    <div class="filter-item">
      <label for="search" class="filter-label">Professor</label>
      <input
        id="search"
        class="filter-item"
        type="text"
        placeholder="Search..."
        @input="emitSearchChanged"
      />
    </div>

    <div class="filter-item">
      <CourseSelect :courses="courses" @onCourseSelected="emitCourseSelected" />
    </div>
  </div>
</template>

<style scoped>
.filter-wrapper {
  display: flex;
  justify-content: center;
  margin-bottom: 20px;
}
.filter-item {
  display: flex;
  flex-direction: column;
  margin-right: 20px;
}
.filter-label {
  margin-bottom: 5px;
  color: var(--color-secondary);
  font-weight: bold;
}
</style>
