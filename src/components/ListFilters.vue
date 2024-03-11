<script setup>
const courses = ['All', 'Math', 'Science', 'English', 'History', 'Geography']

// Emit event in the parent component
const emit = defineEmits(['onSearchChanged', 'onCourseSelected'])

function emitCourseSelected(e) {
  emit('onCourseSelected', e.target.value)
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
      <label for="course" class="filter-label">Category</label>
      <select id="course" class="filter-item" @change="emitCourseSelected">
        <option v-for="(category, idx) in courses" :key="idx" :value="category.toLowerCase()">
          {{ category }}
        </option>
      </select>
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
  margin-right: 20px;
  display: flex;
  flex-direction: column;
}
.filter-label {
  margin-bottom: 5px;
  color: var(--color-secondary);
  font-weight: bold;
}
</style>
