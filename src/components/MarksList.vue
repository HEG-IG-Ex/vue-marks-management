<script setup>
import { computed, ref, onMounted } from 'vue'
import MarkListRow from './MarkListRow.vue'

const sampleMarks = ref([
  { id: 1, date: '2021-09-01', course: 'math', mark: 90, professor: 'John Doe' },
  { id: 2, date: '2021-10-02', course: 'science', mark: 85, professor: 'Jane Smith' },
  { id: 3, date: '2021-11-03', course: 'english', mark: 95, professor: 'Michael Johnson' },
  { id: 4, date: '2021-10-04', course: 'history', mark: 80, professor: 'Sarah Williams' },
  { id: 5, date: '2021-12-10', course: 'geography', mark: 65, professor: 'Robert Brown' },
  { id: 6, date: '2021-10-10', course: 'geography', mark: 75, professor: 'Robert Brown' }
])

const marks = ref([])

// Manage local storage
onMounted(() => {
  loadMarks()
  saveMarks()
})

const loadMarks = () => {
  const savedMarks = localStorage.getItem('marks')
  marks.value = savedMarks ? JSON.parse(savedMarks) : sampleMarks.value
}
const saveMarks = () => {
  localStorage.setItem('marks', JSON.stringify(marks.value))
}

const removeMark = (mark) => {
  console.log(mark)
  const idx = marks.value.indexOf(mark)
  marks.value.splice(idx, 1)
  saveMarks()
}

// Manage filtering
const props = defineProps(['selectedCourse', 'searchQuery'])

const filteredMarks = computed(() => {
  const result = marks.value.filter((mark) => {
    const isAll = props.selectedCourse === 'all'
    if (isAll) {
      return mark.professor.toLowerCase().includes(props.searchQuery.toLowerCase())
    }
    return (
      mark.professor.toLowerCase().includes(props.searchQuery.toLowerCase()) &&
      mark.course.toLowerCase() === props.selectedCourse
    )
  })
  return result
})

// Manage sorting
const sortKey = ref('')
const isAsc = ref(true)
const sortBy = (key) => {
  if (sortKey.value === key) {
    isAsc.value = !isAsc.value
  } else {
    sortKey.value = key
  }
}
const sortedMarks = computed(() => {
  if (sortKey.value) {
    return filteredMarks.value.slice().sort((a, b) => {
      const modifier = isAsc.value ? 1 : -1
      const aValue = a[sortKey.value]
      const bValue = b[sortKey.value]

      // Check if the values are numeric
      if (!isNaN(aValue) && !isNaN(bValue)) {
        return (Number(aValue) > Number(bValue) ? 1 : -1) * modifier
      }

      // If not numeric, compare as strings (case-insensitive)
      return aValue.toString().toLowerCase() > bValue.toString().toLowerCase()
        ? modifier
        : -modifier
    })
  }
  return filteredMarks.value
})
</script>
<template>
  <table class="mark-table">
    <thead>
      <th @click="sortBy('date')">Date</th>
      <th @click="sortBy('subject')">Subject</th>
      <th @click="sortBy('professor')">Professor</th>
      <th @click="sortBy('mark')">Mark</th>
      <th>Action</th>
    </thead>
    <tbody>
      <MarkListRow :marks="sortedMarks" @onRemoveClicked="removeMark" />
    </tbody>
  </table>
</template>

<style scoped>
/* Your component styles here */
.mark-table {
  width: 100%;
  border-collapse: collapse;
}
.mark-table th {
  border-bottom: 1px solid #000;
  padding: 0.5rem;
}
.mark-table th {
  background-color: #f0f0f0;
}
.mark-table th {
  text-align: left;
  font-weight: bold;
  background-color: var(--color-primary);
  color: #ffffff;
}
</style>
