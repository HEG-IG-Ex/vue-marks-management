<script setup>
import { ref } from 'vue'
import { nanoid } from 'nanoid'

import { useRouter } from 'vue-router'
const router = useRouter()

import CourseSelect from './CourseSelect.vue'

const courses = ['All', 'Math', 'Science', 'English', 'History', 'Geography']

function updateCourseSelected(course) {
  console.log(course)
  mark.value.course = course
}

const mark = ref({
  id: nanoid(),
  date: '',
  course: '',
  professor: '',
  mark: ''
})

const marks = ref([])

const submitForm = (e) => {
  e.preventDefault()
  addMark(mark.value)
}

const addMark = (mark) => {
  console.log(mark)

  // Add mark to the store
  loadMarks()
  marks.value.push(mark)
  saveMarks()

  // Reset the form
  mark.value = {
    id: nanoid(),
    date: '',
    course: '',
    professor: '',
    mark: ''
  }

  // Reutn to the home page
  router.push('/')
}

const loadMarks = () => {
  const savedMarks = localStorage.getItem('marks')
  marks.value = savedMarks ? JSON.parse(savedMarks) : []
}
const saveMarks = () => {
  localStorage.setItem('marks', JSON.stringify(marks.value))
}
</script>

<template>
  <form @submit="submitForm">
    <div class="form-group">
      <label for="date">Date</label>
      <input type="date" id="date" v-model="mark.date" required />
    </div>

    <div class="form-group">
      <CourseSelect :courses="courses" @onCourseSelected="updateCourseSelected" />
    </div>

    <div class="form-group">
      <label for="professor">Professor</label>
      <input type="text" id="score" v-model="mark.professor" required />
    </div>

    <div class="form-group">
      <label for="mark">Mark</label>
      <input type="number" id="mark" v-model="mark.mark" required />
    </div>

    <div class="form-button-group">
      <button type="submit">Submit</button>
      <button>Back</button>
    </div>
  </form>
</template>

<style scoped>
form {
  display: flex;
  flex-direction: column;
  gap: 20px;
  max-width: 300px;
  margin: 0 auto;
}
.form-group {
  display: flex;
  flex-direction: column;
}
label {
  margin-bottom: 5px;
  color: var(--color-secondary);
  font-weight: bold;
}
.form-button-group {
  display: flex;
  gap: 20px;
  justify-content: center;
}
.form-button-group button {
  padding: 10px 20px;
  border-radius: 5px;
  border: none;
  background-color: var(--color-primary);
  color: #ffffff;
  cursor: pointer;
}
/* Your component styles here */
</style>
